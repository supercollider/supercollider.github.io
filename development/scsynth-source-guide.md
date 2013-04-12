---
layout: group_index
group: development
title: scsynth
---

This is a guide to the source code of the *scsynth* implementation of the SuperCollider audio server. Note that there is a newer implementation called *supernova*, which shares little source code with *scsynth* (only as far as the plugin and OSC interfaces are concerned).

This is the kind of documentation that could get out of date very quickly. none the less, it might give you a good overview of what does what where in the server. (btw. http://www.doxygen.org was pretty handy while figuring this stuff out)

### Thread structure


Main Thread - main(), this thread blocks waiting on the quit semaphore after initializing the World, which starts the Audio Driver (Audio Thread and Audio Engine NRT Thread), and the Com Ports.

Com Port Thread(s) - one or more threads which listen for incoming OSC messages.

Audio Thread - pumped by host API audio callback

Audio Engine NRT (Non-Real-Time) Thread - launched by audio driver, blocks on a signal from the Audio Thread which is pumped at the end of each audio callback.

Disk I/O thread - launched by DiskIO_UGens.cpp, waits on gDiskFifoHasData, pumps gDiskFifo queue.


### Inter-thread message queues

Audio Thread -> Audio Engine NRT Thread (HiddenWorld::mTriggers, HiddenWorld::mNodeEnds, HiddenWorld::mDeleteGraphDefs, SC_CoreAudioDriver::mFromEngine)

Audio Engine NRT Thread -> Audio Thread (SC_CoreAudioDriver::mToEngine via SC_SequencedCommand::CallNextStage())

Com Port Thread(s) -> Audio Thread (via ProcessOSCPacket() call in SC_TcpConnectionPort::Run(), SC_UdpInPort::Run(), and World_SendPacket)

Audio Thread -> Disk I/O thread (DiskIn_next and DiskOut_next post read and write requests to gDiskFifo)


### File descriptions

#### `[headers,source]/common/`

dfftlib.h

- prototypes for FFT functions (d for double, see also fftlib.h)
	- no header guards (jmc says: borrowed code, not mine)

dlfcn.h/dlopen.c

- Mac implementation of BSD dlopen(), dlsym(), dlerror(), dlclose() dynamic linking interface
	- no header guards (jmc says: borrowed code, not mine)

fftlib.h

- prototypes for FFT functions
x- no header guards (jmc says: borrowed code, not mine)

SC_AllocPool.h/SC_AllocPool.cpp

- A memory allocator, parameterised by functions which alocate and free "Areas" (pages).
- World uses an AllocPool (stored in the HiddenWorld) to implement the so-called "real-time memory allocator", a memory pool with a large initial size that is only used by the real-time thread. Used instead of malloc because malloc might take a mutex which cannot be allowed to happen in the audio callback.

SC_Altivec.h

- altivec utility functions
- defines USEVEC

SC_Endian.h

- checks that BIG_ENDIAN or LITTLE_ENDIAN is defined
- includes or defines htonl, htons, ntohl, ntohs

SC_Sem.h/SC_Sem.cpp

	Semaphore{
		Semaphore( initialCount );
		void Aquire();
		voir Release();
	}

- Semaphore abstraction implemented using pthreads


SC_StringParser.h/SC_StringParser.cpp

- String tokeniser parameterised by separator. NextToken() returns successive tokens. SC_MAX_TOKEN_LENGTH limits token length. Uses internal buffer to temporarily hold the returned token.

scsynthsend.h/scsynthsend.cpp

- implements the scpacket class, a utility for constructing and and sending OSC packets
- includes implementation of makeSockAddr which perhaps could be static
- calls external functions sendallto() and mentions (but dosn't use) sendall()


#### headers/plugin_interface/

clz.h

- count leading zeros macro and derived functions
- uses inline asm for count leading zeros instruction

Hash.h

- inline hashing functions for strings and integers

SC_BoundsMacros.h

- abs, min, max and clip macros

SC_BufGen.h

- BufGen structure and function
- BufGen_Create function

SC_Constants.h

- math constants like pi, 2pi, log01 etc.

SC_Dimension.h

- SC_Dimension struct contains width, height, numPixels, xslope, yslope
- was used in SC3d5 on MacOS 9 for the image processing unit generators. not used now (or yet).

SC_FifoMsg.h

- Fifo message struct calls Perform() and Free() funcs, contains a data and a world ptr

SC_Graph.h

- graph structure

SC_InlineBinaryOp.h

- optimised inline functoins for common math and nunmeric operations

SC_InlineUnaryOp.h

- optimised inline functions for common math and interpolation

SC_InterfaceTable.h

- table of function pointers to World functions callable from plugins

sc_msg_iter.h

- implements sc_msg_iter class for parsing and decoding OSC packets

SC_Node.h

- node structure
- see source/server/SC_Node.cpp

SC_PlugIn.h

- global include file for plugins, inclues all other necessary include files

SC_Rate.h

- Rate struct containing values derived from rate such as inverses/radian rate etc.
- see source/server/SC_Rate.cpp

SC_RGen.h

- Tausworthe PRNG implemented with inline functions

SC_SndBuf.h

- SndBuf struct and inline lookup functions

SC_Types.h

- basic type definitions such as int8, uint8, int64 etc

SC_Unit.h

- unit structure and field accessor macros
- see source/server/SC_Unit.cpp

SC_Wire.h

- Wire structure
- a Wire is a connection between unit generators

SC_World.h

- plugin-visible World structure
- contains constants and values used by plugins
- contains pointer to InterfaceTable
- see source/server/SC_World.cpp

SC_WorldOptions.h

- structure containing parsed command line options

Unroll.h

- macros and utilities for implementing optimized loops


#### headers/server/

HashTable.h

- implementation of HashTable and IntHashTable container templates

IntFifo.h

- single reader, single writer, fixed length FIFO of ints template

MsgFifo.h

- message FIFO templates: MsgFifo, MsgFifoNoFree contains a fixed number of messages. calls Perform() and Free() on enqueued messages.

OSC_Packet.h

- OSC_Packet structure, header data for an OSC packet

PriorityQueue.h

- PriorityQueue container template

ReadWriteMacros.h

- functions for reading and writing specified byte-ordered values to and from buffers and ansi FILEs

SC_HiddenWorld.h

- global gUnitDefLib hash table
- TriggerMsg, NodeEndMsg and DeleteGraphDefMsg structs
- HiddenWorld struct contains data private to the World implementation

SC_List.h

- doubly linked list container template

SC_Lock.h

	SC_Lock{
		void Lock();
		void Unlock();
	}

- SC_Lock abstraction, wraps pthreads mutex


SC_Prototypes.h

- Prototypes for free functions pertaining to World, GraphDef, Graph, Node, Group, Unit


SC_Reply.h

- ReplyAddress struct and SendReply functions


SC_SynthDef.h

- NodeDef struct, extern gGroupNodeDef
- prototypes for GroupNodeDef_Init and NodeDef_Dump

SC_UnitSpec.h

- struct UnitSpec

SC_WireSpec.h

- struct InputSpec, struct OutputSpec

Rendezvous.h/Rendezvous.cpp

- function to publicise the SC server as a Rendezvous net service (calls CFNetServiceCreate(), CFNetServiceRegister).

#### headers/server/SC_Samp.h
- prototypes and global wavetables as defined in Samp.cpp

Samp.cpp

- more or less duplicated in lang
- global sine wavetables: gSine, gPMSine, gInvSine, gSineWavetable
- implements SignalAsWavetable()/WavetableAsSignal() which encode wavetables in some interesting way

SC_BufGen.cpp

- implements BufGen_Create() which hashes the gen name and creates a new BufGen object (binding a BufGen function) and registers it by calling AddBufGen (implemented in SC_World.cpp)

SC_Carbon.cpp

- implements HasAltivec() using Carbon Gestalt, comment asks how to implement on Linux.

SC_Complex.h/SC_Complex.cpp

- classes Polar and Complex with conversion functions. global lookup tables gMagLUT, gPhaseLUT

SC_ComPort.h/SC_ComPort.cpp

- NOTE: this is different from the implementation in lang (although many of the differences are questionable)
- OSC socket listeners / dispatchers
- implements CmdPort heirarchy including ComPort, SC_TcpConnectionPort, SC_TcpInPort, SC_UdpInPort
- when Start()ed these classes create a new thread and run a loop waiting for new messages.
- SC_TcpInPort listens on a TCP socket and creates a new SC_TcpConnectionPort to handle requests on a connection
- SC_UdpInPort and SC_TcpConnectionPort listen for OSC messages and send them to ProcessOSCPacket(packet)
- contains comment about potential delete this; crash
- implements World_SendPacket

SC_CoreAudio.h/SC_CoreAudio.cpp

- defines SC_AudioDriver base struct (seems to not contain everything it should)
- implements interface to audio driver (CoreAudio, JACK)
- implements engine functionality (pumps queues, calls the World to generate audio)

SC_Dimension.cpp

- initialization function for SC_Dimension struct (perhaps could be a class but isn't)

SC_Errors.h/SC_Errors.cpp

- error code enumeration
- SC_ErrorString() - converts error codes to strings

SC_Graph.cpp

- implements functions of SC_Graph struct
- is a Node
- a tree of Nodes
- a Graph is a leaf node (Groups are internal nodes).

SC_GraphDef.h/SC_GraphDef.cpp

- implements function of SC_GraphDef struct (could be a class?)
- Prototype for a Graph

SC_Group.h/SC_Group.cpp

- is a Node
- a linked list of Nodes which are executed in order
- Groups are internal nodes.

headers/server/SC_Lib.h

- SC_NamedObj class, GetKey() and GetHash()

source/server/SC_Lib.cpp

- utility functions for sending /done /fail and /late OSC packets
- implementation of NamedObject
- implementation of SC_LibCommand (Command pattern wrapper for function ptr with exception -> error result conversion).
- implements NewCommand function which registers the commands with gCmdLib and gCmdArray - with a name or command number. this seems to be for calling LibCommands from OSC

headers/server/SC_Lib_Cintf.h

- struct SC_LibCmd
- gCmdLib hash table
- gCmdArray command array
- command number enumerations

source/server/SC_Lib_Cintf.cpp

- implements initalize_library() function which creates gCmdLib, gUnitDefLib, gBufGenLib, gPlugInCmds
- iterates plugins in the plugin directory
- calls each plugins `_load` function.

SC_MiscCmds.cpp

- implementation and registration of many server commands

SC_Node.cpp

- implementation of Node functions

SC_Rate.cpp

- Rate struct initializer - calculates derived values from sample rate and buffer size

SC_SequencedCommand.h/SC_SequencedCommand.cpp

- implements SC_SequencedCommand and subclasses BufGenCmd, BufAllocCmd, BufShmAllocCmd, BufFreeCmd, BufCloseCmd, BufZeroCmd, BufAllocReadCmd, BufReadCmd, BufWriteCmd, AudioQuitCmd, AudioStatusCmd, NotifyCmd, LoadSynthDefCmd, RecvSynthDefCmd, LoadSynthDefDirCmd, SendReplyCmd
- SequencedCommands execute in up to four stages Stage1(), Stage2(), Stage3(), Stage4()
- from the header file:
Having SequencedCommands allows performing actions that might otherwise require
taking a mutex, which is undesirable in a real time thread.
Some commands require several stages of processing at both the real time
and non real time levels. This class does the messaging between levels for you
so that you only need to write the functions.


SC_Str4.h/SC_Str4.cpp

- 4-byte aligned and zero padded string functions

SC_SyncCondition.h/SC_SyncCondition.cpp

- implements SC_SyncCondition, and implementation of a condition variable synchronisation primitive
- uses pthread pthread_cond_t and pthread_mutex_t

SC_Unit.cpp

- Unit struct functions
- includes Unit_New which initialises a Unit from a UnitSpec


headers/server/SC_UnitDef.h

- struct PlugInCmd, UnitCmd and UnitDef
- prototypes for UnitDef_Create, UnitDef_AddCmd and PlugIn_DefineCmd

source/server/SC_UnitDef.cpp

- Create UnitDef
- functions for registering PlugIn and Unit commands

SC_World.cpp

- implementation of the World object, the top level SC server object. World is basically a container for the various buses, queues, hash tables and buffers. The world contains the top Group. World creates an SC_CoreAudioDriver to perform the realtime synthesis. Implementation details of SC_World which are not visible to plugins are stored in the HiddenWorld structure.
- offline synthesis
- initializer for struct InterfaceTable
- free function wrappers for:
- memory allocation in the World's pool
- hashing, registering and removing world graph defs
- hashing, registering and removing unit defs
- hashing, registering and removing buf gens
- hashing, registering and removing plugin cmds
- hashing, adding, removing and looking up Nodes, Graphs and Groups
. note that all of the above overload GetKey and GetHash based on parameter type
- some sample format detection functions
- Perform() implementations for TriggerMsg, NodeEndMsg, DeleteGraphDefMsg
- implementation of NotifyNoArgs()
- implementation of free func SendMsgToEngine(), SendMsgFromEngine()
- implementation of SetPrintFunc and scprintf()

scsynth_main.cpp

- parse command line options into WorldOptions struct, detect missing args
- create World instance
- open UDP and TCP listeners if requested
- call World_WaitForQuit to execute


#### source/plugins

SCComplex.c/SCComplex.h

- Note these are not the same as `SC_Complex.[c,h]` in the server
- Defines SCComplex and SCPolar structs.
- It is questionable whether these files and the ones used by the server (`SC_Complex.[c,h]`) should be different.

