---
template: home.html
hide:
  - toc
  - navigation
---

<style>
article > h1 {
    display: none
}

body > header > nav > div.md-header__title.md-header__title--active > div > div:nth-child(2){
    font-weight: 700;   
}
.package-icon{
    width: 5rem;
}
body > div.md-container > main > div > div > article > a{
    display: none
}

.md-main__inner > .md-content > article {
    margin-top: 0 !important;
    padding-top: 0 !important;
}

article h1 {
    margin-bottom: 0.8rem;
}
article p {
    margin-top: 0.5rem;
    margin-bottom: 1rem;
}


</style>

<div style="text-align: center;">

<img class="package-icon skip-glightbox" src="assets/images/package.png">
  <h1>Information of PGTEC</h1>
  
</div>

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
