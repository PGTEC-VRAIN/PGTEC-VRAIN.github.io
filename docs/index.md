---
template: home.html
hide:
  - toc
  - navigation
---

<style>
/* Hide title on the home page */
article > h1 {
    display: none
}

/* Fix title font-weight */
body > header > nav > div.md-header__title.md-header__title--active > div > div:nth-child(2){
    font-weight: 700;   
}
.package-icon{
    width: 5rem;
}
body > div.md-container > main > div > div > article > a{
    display: none
}
</style>

<div style="text-align: center;">

<img class="package-icon skip-glightbox" src="assets/images/package.png">
  <h1>Minimal Package for TEF nodes</h1>
  <p>Work package 3 (WP3) provides the <strong>Minimal Package for PGTEC (Testing and Experimentation Facility) nodes</strong>, which contains comprehensive <strong>guides, toolboxes, and deployment frameworks</strong> to ensure interoperability across the wide range of TEF nodes by defining a <strong>common reference architecture</strong>. Based on this architecture, it also provides support and examples to develop <strong>AI services</strong>.</p> 
</div>

<br>
### Package components

<div class="grid cards cols-3" markdown>

- :material-rocket-outline: **Introduction**

    Start by learning the basics of PGTEC.

    [:octicons-arrow-right-24: Learn more](welcome.md)

- :material-store-search-outline: **Data sources**

    Information on data sources relevant to climate emergency management.   

    [:octicons-arrow-right-24: Learn more](data_sources/index.md)

- :material-tools: **Data pipeline**

    Data pipeline to query the APIs every x amount of time

    [:octicons-arrow-right-24: Learn more](pipeline/index.md)

</div>
