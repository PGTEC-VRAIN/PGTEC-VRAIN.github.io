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
    <p>A data platform that periodically retrieves <strong>climate</strong>  and <strong>weather</strong> historical data and predictions from multiple APIs, standardizes them using <strong>Smart Data Models</strong> and stores them in a <strong>FIWARE Context Broker</strong> with historical persistence for machine learning and deep learning models.</p> 
</div>

<div class="grid cards cols-3" markdown>

- :material-rocket-outline: **Getting started**

    Start by learning the basics of PGTEC.

    [:octicons-arrow-right-24: Learn more](getting_started/index.md)

- :material-database: **Data Sources**

    Information of data sources for climate emergency management.   

    [:octicons-arrow-right-24: Learn more](data_sources/index.md)

- :material-sitemap-outline: **Data Flow**

    The guide of a complete environment for the project.

    [:octicons-arrow-right-24: Learn more](pipeline/index.md)

- :material-puzzle-outline: **Smart Data Models**  

    Description of the data models used

    [:octicons-arrow-right-24: Learn more](SmartDataModels/index.md)

</div>
