---
layout: default
title: Task
parent: Getting Started
nav_order: 1
---

## Task

A **task** in AWPL represents a unit of computation or data processing within a workflow or data pipeline. Tasks are the fundamental building blocks of AWPL and can perform a wide variety of operations, such as:

- Reading or writing data from external sources,
- Executing computations or transformations (like filtering, aggregating, joining), and
- Logging or monitoring.

Each task is uniquely identified by its `id` and can optionally include a `description` for documentation purposes. Tasks can also define dependencies on other tasks (`depends_on`) and task-specific configurations (`task_config`), allowing AWPL to manage execution order automatically.

```yaml
task: 
  id: "identifier"
  description: "description"
  depends_on:
    - "identifier"
  task_config: ...
```

#### Arguments

| Name              | Type   | Required | Default | Description                              |
|-------------------|--------|----------|---------|------------------------------------------|
| `id`              | string | yes      | –       | Unique identifier of the task.           |
| `description`     | string | no       | ""      | Optional description of the task.        |
| `depends_on`      | list   | no       | []      | List of task IDs this one depends on.    |
| `task_config`     | object | yes      | -       | see [here]({% link configuration.md %}). |

