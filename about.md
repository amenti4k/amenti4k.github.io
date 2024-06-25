---
layout: default
---

<div class="about">
    <h1>About</h1>

    <pre><code>~/about.yml</code></pre>

    <pre><code>Amenti Kenea
residence: San Francisco, US
----
Born and raised in Addis Ababa, Ethiopia. 
College @Minerva living in 7 countries. 
Internships @raiseme, microsoft, contrary-capital, & facebook.
Currently data-scientist @meta.
Chronically online. 
</code></pre>

    <pre><code>~/presentation.txt</code></pre>

    <div class="blink-text">█ ████████</div>
</div>

<style>
    .about {
        font-family: monospace;
        line-height: 1.6;
    }
    .about h1 {
        font-size: 1.5em;
        margin-bottom: 20px;
    }
    .about pre {
        background-color: #f4f4f4;
        padding: 10px;
        border-radius: 5px;
        overflow-x: auto;
    }
    .about code {
        display: block;
        white-space: pre-wrap;
    }
    .blink-text {
        animation: blink 1s step-end infinite;
    }
    @keyframes blink {
        50% { opacity: 0; }
    }
</style>
