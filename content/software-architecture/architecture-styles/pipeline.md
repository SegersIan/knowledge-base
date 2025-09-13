[<< Back To Overview](./readme.md)

# Architecture Style: Pipeline

![Pipeline Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1101.png)

*Alternative names: Pipes and filters*

## Description

Known as the underlying principle behind Unix terminal shell languages, those who dabble in functional programming will also see parallel's. MapReduce is also a popular concept following this style. An entire **process** is built up from pipes and filters to deliver a certain functionality.

The power of **composition** is key in this architectural style.

[See Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1102.png)

### Pipes & Filters

* **Pipes**: Communication channel between filters. Usually unidirectional and point-to-point. Any type of data can be passed on, but small parts are favoured for high performance.
* **Filters**: Self-contained, independent, generally stateless pieces of code that perform a single task (responsibility). A composition of the logic should be done by a sequence of filters. There are 4 types:
    * *Producer*: Starting point of a process. (AKA the "source")
    * *Transformer*: Takes input and transforms the input from the upstream pipe in some way and forwards it to the downstream pipe.
        * A *map* in functional programming.
    * *Tester*: Takes input from the upstream pipe and tests certain criteria (e.g. business logic), optionally producing output on the downstream pipe.
        * A *reduce* in functional programming.
    * *Consumer*: End of the process pipeline. The final result can be persisted or displayed.


## When To Use

* When there is one-way data processing.
* For data pipelines or event pipelines such as ETL (Extract, Transform, and Load) for data warehousing and analytics.
* Orchestration of processes.

## When NOT To Use

By default don't use it, unless the "reasons to use" are clearly met.

## Considerations

This is still a monolithic style, so it comes with all the flaws of monolithic architectures.

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Partitioning Type | Technical    |
| Number of quanta  | 1            |
| Deployability     | ⭐⭐        |
| Elasticity        | ⭐           |
| Evolutionary      | ⭐⭐⭐      |
| Fault Tolerance   | ⭐           |
| Modularity        | ⭐⭐⭐      |
| Overall cost      | ⭐⭐⭐⭐⭐ |
| Performance       | ⭐⭐        |
| Reliability       | ⭐⭐⭐      |
| Scalability       | ⭐           |
| Simplicity        | ⭐⭐⭐⭐⭐ |
| Testability       | ⭐⭐⭐      |

## Resources

* [More shell, less egg](http://www.leancrew.com/all-this/2011/12/more-shell-less-egg/)