---
layout:     post
title:      Yarn内存/CPU分配方案模板
categories: yarn hadoop
summary:	以horntonworks给出推荐配置为蓝本，给出一种常见的Hadoop集群上各组件的内存分配方案。
---

以horntonworks给出推荐配置为蓝本，给出一种常见的Hadoop集群上各组件的内存分配方案。

## 内存分配参考方案

|-------------------------------------+---------------------+----------------|
| Configuration Setting               | Value Calculation   | 64GB RAM Host  |
|-------------------------------------|---------------------|----------------|
| yarn.nodemanager.resource.memory-mb | = containers * RAM-per-container | 32GB |
|-------------------------------------+---------------------+----------------|
| yarn.scheduler.minimum-allocation-mb | = RAM-per-container | 8GB |
|-------------------------------------+---------------------+----------------|
| yarn.scheduler.maximum-allocation-mb | = containers * RAM-per-container | 32GB |
|---+---+---|
| mapreduce.map.memory.mb | = RAM-per-container | 8GB |
|---+---+---|
| mapreduce.reduce.memory.mb | = 2 * RAM-per-container | 16GB |
| mapreduce.map.java.opts | = 0.8 * RAM-per-container | 6.4GB |
|---+---+---|
| mapreduce.reduce.java.opts | = 0.8 * 2 * RAM-per-container | 12.8GB |
|---+---+---|
| yarn.app.mapreduce.am.resource.mb | = 2 * RAM-per-container | 16GB |
|---+---+---|
| yarn.app.mapreduce.am.command-opts | = 0.8 * 2 * RAM-per-container | 12.8GB |
|---+---+---|

## CPU分配参考方案

|-------------------------------------+---------------------+----------------|
| Configuration Setting               | Value Calculation   | 24 Cores CPU Host  |
|-------------------------------------|---------------------|----------------|
| yarn.app.mapreduce.am.resource.cpu-vcores | = CPU-cores-per-container   | 4 |
|---+---+---|
| mapreduce.map.cpu.vcores                  | = CPU-cores-per-container   | 4 |
|---+---+---|
| mapreduce.reduce.cpu.vcores               | = CPU-cores-per-container   | 4 |
|---+---+---|
| yarn.nodemanager.resource.cpu-vcores      | = containers * CPU-cores-per-container | 16 |
|---+---+---|
| yarn.scheduler.minimum-allocation-vcores  | = 0.5 * CPU-cores-per-container | 2 |
|---+---+---|
| yarn.scheduler.maximum-allocation-vcores  | = CPU-cores-per-container   | 16 |
|---+---+---|
