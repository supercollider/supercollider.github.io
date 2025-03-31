---
layout: page
title: Downloads
bootstrap: true
---

Stable Releases, Betas, Release Candidates and Development builds are accessible via [GitHub releases](https://github.com/supercollider/supercollider/releases).

<ul class="nav nav-tabs" id="osTab" role="tablist">
    {% for os in site.data.downloads.os %}
        <li class="nav-item" role="presentation">
            <button
                class="nav-link {% if forloop.first %}active{% endif %}"
                id="{{ os.slug | downcase }}-tab"
                data-toggle="tab"
                data-target="#{{ os.slug | downcase }}"
                type="button"
                role="tab"
                aria-controls="{{ os.slug }}"
                aria-selected="true"
            >{{ os.slug }}
            </button>
        </li>
    {% endfor %}
    <li class="nav-item" role="presentation">
        <button
            class="nav-link"
            id="other-tab"
            data-toggle="tab"
            data-target="#other"
            type="button"
            role="tab"
            aria-controls="Other releases"
            aria-selected="true"
        >Other releases
        </button>
    </li>
    <li class="nav-item" role="presentation">
        <button
            class="nav-link"
            id="extensions-tab"
            data-toggle="tab"
            data-target="#extensions"
            type="button"
            role="tab"
            aria-controls="Plugins And Extensions"
            aria-selected="true"
        >Plugins And Extensions
        </button>
    </li>
</ul>

<div class="tab-content" id="osTabContent">
    {% for os in site.data.downloads.os %}
        <div
            class="tab-pane fade {% if forloop.first %}show active{% endif %}"
            id="{{ os.slug | downcase }}"
            role="tabpanel"
            aria-labelledby="{{ os.slug }}-tab"
        >
            {% for category in os.categories %}
                <b>{{ category.name | capitalize }}</b>
                <p>{{ category.start_text }}</p>
                <ul>
                    {% for download in category.downloads %}
                        <li>
                            <a href="{{ download.link }}">
                            {{ download.name }}
                            </a>
                        </li>
                    {% endfor %}
                </ul>
                <p>{{ category.end_text }}</p>
            {% endfor %}
        </div>
    {% endfor %}
    <div
        class="tab-pane fade"
        id="other"
        role="tabpanel"
        aria-labelledby="other-tab"
    >
        <b>Sources</b>
        <p>
            Build instruction can be found on <a href="https://github.com/supercollider/supercollider">GitHub</a> in the README corresponding to your Operating System.
        </p>
        <b>Other Platforms</b>
        <p>
            SuperCollider can be used on embedded platforms, including Raspberry Pi and Beagle Bone Black.
            See the <a href="https://github.com/supercollider/supercollider">project READMEs</a> for more information.
        </p>
    </div>
    <div
        class="tab-pane fade"
        id="extensions"
        role="tabpanel"
        aria-labelledby="extensions-tab"
    >
        <b>SC3 Plugins</b> 
        <p>
            <a href="https://supercollider.github.io/sc3-plugins">https://supercollider.github.io/sc3-plugins</a>
        </p>
        <p>
            The sc3-plugins are extension plugins for the SuperCollider audio synthesis server.<br/>
            These third-party plugins provide additional synthesis, analysis, and other capabilities for the sound server.
        </p>
        <hl/>
        <b>Quarks</b><br/>
        <p>
            <a href="https://github.com/supercollider-quarks/quarks">https://github.com/supercollider-quarks/quarks</a>
        </p>
        <p>
            Quarks are packages containing classes, extension methods, documentation and UGens.<br/>
            The integrated Quarks package system is used to download and manage these packages on your system.
        </p>
    </div>
</div>
