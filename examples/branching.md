---
layout: default
title: Branches
parent: Examples
nav_order: 1
---

```yaml
name: BranchingExample
description: Example airflow application containing two if constructs
pipeline_config:
  schedule: "@daily"
  start_date: '2025-09-20T00:00:00Z'
  catchup: false

nodes:
  - id: "task_1"
    type: "task"
    description: "Entry task"
    task_config: ...
  - id: "task_2"
    type: "task"
    description: "Second task"
    depends_on:
      - "task_1"
    task_config: ...
  - id: "branch_1"
    type: "branch"
    description: "Conditional check"
    condition: 
      combinedWith: "and"
      conditions:
        - lhs: "task_2.output1"
          rhs: "10"
          operator: ">"
          negation: false
        - lhs: "task_1.output3"
          rhs: "10"
          operator: ">"
          negation: true
    branches:
      true:
        - id: "loop_1"
          type: "loop"
          description: "Sequential Loop"
          condition:
            combinedWith: "and"
            conditions:
              - lhs: "loop_data"
                rhs: "10"
                operator: ">"
                negation: false
          loop_data:
            id: "loop_data"
            init: "task_2"
            loop: "task_4"
          body:
            - id: "task_3"
              type: "task"
              description: "First loop task"
              task_config: ...
            - id: "task_4"
              type: "task"
              description: "Second loop task"
              depends_on:
                - "task_3"
              task_config: ...
      false:
        - id: "task_4"
          description: "Branch false task"
          depends_on:
            - "task_1"
          task_config: ...
      depends_on:
        - "task_2"
  - id: "parallel_loop_1"
    type: "parallelLoop"
    over: "branch_1"
    body: 
      - id: "task_5"
        type: "task"
        description: "First parallel loop task"
        task_config: ...
      - id: "task_6"
        type: "task"
        description: "Second parallel loop task"
        depends_on:
          - "task_5"
        task_config: ...
```
