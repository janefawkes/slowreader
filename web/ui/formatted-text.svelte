<script lang="ts">
  /* We escape and have XSS tests */
  /* eslint svelte/no-at-html-tags: "off" */

  import { sanitizeDOM } from '@slowreader/core'

  export let html: string

  let node: HTMLDivElement | undefined

  $: if (node) {
    node.innerHTML = ''
    node.replaceChildren(...sanitizeDOM(html).childNodes)
    let links = node.querySelectorAll('a')
    links.forEach(link => {
      link.setAttribute('target', '_blank')
      link.setAttribute('rel', 'noopener')
    })
  }
</script>

<div bind:this={node} class="formatted-text"></div>

<style>
  .formatted-text {
    overflow-x: auto;
    text-wrap: pretty;
  }

  .formatted-text :global(img) {
    max-width: 100%;
    height: auto;
    padding: 0.3em 0;
    margin: 0 auto;
  }

  .formatted-text :global(p) {
    margin: 0 0 0.8em;
  }

  .formatted-text :global(h1),
  .formatted-text :global(h2),
  .formatted-text :global(h3),
  .formatted-text :global(h4),
  .formatted-text :global(h5),
  .formatted-text :global(h6) {
    margin: 1.6em 0 0.8em;
    font-weight: bold;
  }

  .formatted-text > :global(h1:first-child),
  .formatted-text > :global(h2:first-child),
  .formatted-text > :global(h3:first-child),
  .formatted-text > :global(h4:first-child),
  .formatted-text > :global(h5:first-child),
  .formatted-text > :global(h6:first-child) {
    margin-top: 0;
  }

  .formatted-text :global(h1) {
    font: var(--card-title-font);
  }

  .formatted-text :global(h2) {
    font-size: 1.429em;
    line-height: 1.2;
  }

  .formatted-text :global(h3) {
    font-size: 1.296em;
    line-height: 1.2;
  }

  .formatted-text :global(h4) {
    font-size: 1.215em;
    line-height: 1.2;
  }

  .formatted-text :global(h5) {
    font-size: 1.138em;
  }

  .formatted-text :global(h6) {
    font-size: 1em;
  }

  .formatted-text :global(a) {
    color: var(--link-color);
    word-wrap: break-word;
    opacity: 100%;
  }

  .formatted-text :global(a:visited) {
    color: var(--link-color-visited);
  }

  .formatted-text :global(a:hover) {
    opacity: 85%;
  }

  .formatted-text :global(a:active) {
    opacity: 87%;
  }

  .formatted-text :global(em) {
    font-style: italic;
    font-weight: 600;
  }

  .formatted-text :global(ul) {
    padding-inline-start: 1.25em;
    list-style-type: disc;
  }

  .formatted-text :global(ol) {
    padding-inline-start: 1.25em;
    list-style-type: decimal;
  }

  .formatted-text :global(li) {
    margin-bottom: 0.625em;
  }

  .formatted-text :global(blockquote) {
    padding: 0.625em 1.25em;
    margin: 0 0 1.25em;
    border-inline-start: 0.3125em solid var(--border-color);
  }

  .formatted-text :global(caption) {
    padding: 0.625em;
    font-style: italic;
    text-align: center;
  }

  .formatted-text :global(figcaption) {
    font-style: italic;
    text-align: center;
  }

  .formatted-text :global(dd) {
    margin-inline-start: 2.5em;
  }

  .formatted-text :global(video) {
    display: block;
    max-width: 100%;
    height: auto;
    margin: 0 auto;
  }

  .formatted-text :global(audio) {
    display: block;
    width: 100%;
    margin: 1em 0;
  }

  .formatted-text :global(pre) {
    padding: 1em;
    margin: 0.8em 0;
    overflow-x: auto;
    background-color: var(--field-color);
    border-radius: 4px;
    box-shadow: var(--field-shadow);
  }

  .formatted-text :global(code) {
    padding: 0.3em;
    line-height: 1.8;
    border-radius: var(--radius);
  }

  .formatted-text :global(pre code) {
    max-width: 100%;
    padding: 0.1em 0.25em;
    font-size: 0.89em;
    background: transparent;
  }

  .formatted-text :global(p code) {
    padding: 0.2em 0.4em;
    font-size: 85%;
    white-space: break-spaces;
    background-color: var(--inline-code-color);
    border-radius: 6px;
  }

  .formatted-text :global(table) {
    width: 100%;
    margin: 1em 0;
    border-collapse: collapse;
  }

  .formatted-text :global(td) {
    padding: 0.8em;
    border: 1px solid var(--border-color);
  }

  .formatted-text :global(th) {
    padding: 0.8em;
    border: 1px solid var(--border-color);
  }

  .formatted-text :global(tr) {
    border-bottom: 1px solid var(--border-color);
  }

  .formatted-text :global(col) {
    border: 1px solid var(--border-color);
  }

  .formatted-text :global(colgroup) {
    border: 1px solid var(--border-color);
  }
</style>
