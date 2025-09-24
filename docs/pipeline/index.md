---
icon: material/store-search-outline
title: Data pipeline
hide:
  - toc
---

<script>
    // Hide sidebar. This script is only executed in the data sources page.
    document.addEventListener('DOMContentLoaded', function () {
        const sidebar = document.querySelector('.md-sidebar--secondary');
        if (document.querySelector('.catalog-header') && sidebar) {
            sidebar.style.display = 'none';
            sidebar.style.width = '0';
            sidebar.style.padding = '0';
            sidebar.style.margin = '0';
        }
    });
</script>
