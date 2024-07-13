---
title: SpringBoot JDBC Reverse Analysis
date: 2024-07-13
showToc: false
tags: 
- Spring
- Java
- Jdbc
cover:
  image: img/feature-location-model.svg
---

---

> This is some of my thinking about the Spring framework's JDBC from my reverse engineering course. The `location model` image shows the abstract classes, implementation classes, interfaces, and methods that are directly or indirectly involved when executing the query method. The `workflow` image depicts the detailed function call process after initiating the JDBC query method. 

> Due to space and time limitations, other branches resulting from polymorphism are not shown; only the chain produced by importing SQL of string type is displayed here.


![Img](feature-workflow-model.svg)