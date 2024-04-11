---
layout: markdown
title: Node Hardware
permalink: /hardware
subheader: 
---


<style type="text/css">
  #setup-diagram {
    position: relative;
    width: 100%;
  }
  #diagramLight {
    display: block;
  }
  #diagramDark {
    display: none;
  }
  .dark-mode #diagramLight {
    display: none;
  }
  .dark-mode #diagramDark {
    display: block;
  }

  .component-highlight {
    position: absolute;
  }
  /*.component-highlight:hover,
  .component-highlight:focus,
  .component-highlight:active {
    background-color: rgba(var(--brand-color-1-rgb),0.25);
    border: 2px solid #000;
  }*/
  .component-highlight.active {
    background-color: rgba(var(--brand-color-1-rgb),0.25);
    border: 2px solid #000;
  }
  #component-1 {
    inset: 14% 68% 53% 5%;
  }
  #component-2 {
    inset: 8% 35% 58% 52%;
  }
  #component-3 {
    inset: 14% 7% 52% 65%;
  }
  #component-4 {
    inset: 29% 39% 34% 37%;
  }
  #component-5 {
    inset: 58% 25% 5% 57%;
  }
  #component-6 {
    inset: 57% 1% 4% 79%;
  }
  
  .component-details {
    position: absolute;
    inset: 66% 43% 0% 0%;
    background-color: var(--bs-body-bg);
    /*border: 1px solid var(--bs-body-color);*/
    /*padding: 1rem;*/
    opacity: 0;
  }
  {%- for component in site.data.hardware -%}
    #component-{{component.index}}.active ~ #details-{{component.index}} {
      opacity: 1 !important;
    }
  {%- endfor -%}
</style>


<div id="setup-diagram">
  <img id="diagramLight" src="/assets/img/hardware/setup-original.png" style="max-height:100%;">
  <img id="diagramDark" src="/assets/img/hardware/setup-original-dark.png" style="max-height:100%;">
  {%- for component in site.data.hardware -%}
    <div id="component-{{component.index}}" class="component-highlight"></div>
    <div id="details-{{component.index}}" class="component-details">
    <p><u><strong>{{component.name}} ({{component.usage | titlecase}})</strong></u></p>
    {%- for item in component.products -%}
      &#x2022; <a href="{{item.link}}">{{item.name}}</a><br>
    {%- endfor -%}
    <!-- <table class="d-none table nonresponsive">
      <thead>
        <tr>
          <th>Option</th>
          <th>Cost</th>
        </tr>
      </thead>
      <tbody>
        {%- for item in component.products -%}
          <tr>
            <td><a href="{{item.link}}">{{item.name}}</a></td>
            <td>~${{item.price}}</td>
          </tr>
        {%- endfor -%}
      </tbody>
    </table> -->

    </div>
  {%- endfor -%}
</div>
<br>

<script type="text/javascript">

  document.querySelectorAll(".component-highlight").forEach(el => {
    el.addEventListener('click',function (e) {
      console.log(this.id);
      removeHighlights();
      this.classList.add("active");
    });
    el.addEventListener('mouseover',function (e) {
      console.log(this.id);
      removeHighlights();
      this.classList.add("active");
    });
  });
  document.addEventListener("click", function(e) {
    if (!e.target.classList.contains("component-highlight")) {
      removeHighlights();
    }
  });

  function removeHighlights() {
    document.querySelectorAll(".component-highlight").forEach(el => {
      el.classList.remove("active");
    });
  }
</script>



{% assign total_price = 0 %}

{:class="table"}
Item | Component  | Product | Price | Notes
-----|------------|---------|-------|-------
{% for component in site.data.hardware %}
  {%- assign item = component.index -%}
  {%- assign name = component.name -%}
  {%- assign product0 = component.products[0] -%}
  {%- assign product = product0.name -%}
  {%- assign link = product0.link -%}
  {%- assign price = product0.price -%}
  {%- assign total_price = total_price | plus: price -%}
  {%- capture product_link -%}
    [{{product}}]({{link}})
  {%- endcapture -%}
  {%- if product0.name == "Any" -%}
    {%- assign product_link = product -%}
  {%- endif -%}
  {%- assign notes = component.usage | titlecase -%}
  {{item}} | {{name}} | {{product_link}} | ${{price}} | {{notes}}
{% endfor %}




### #StakeFromHome

Check out the [#StakeFromHome gallery](https://bafybeidlhoas5o3thlzjgei3gkxgwgcyvv7hgofaknxl6cgv7gbw5nwqoq.ipfs.nftstorage.link/) to view other node operator setups or share your setup with others by tweeting out an image with the #StakeFromHome hashtag!








