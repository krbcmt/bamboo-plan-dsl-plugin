---
title: Deployment projects
position: 1.0
right_code: |
  ~~~groovy
  plan(key: 'SIMPLEPLAN', name: 'my simple plan') {
      deploymentProject(name: 'DP1', id: 1) {
          description 'my deployment project'
          useCustomPlanBranch 'PLAN_BRANCH_NAME'

          environment(name: 'staging', id: 1) {
              description 'Staging env'
          }
          environment(name: 'prod', id: 2) {
              description 'Production env'
          }
          releaseVersioning(nextReleaseVersion: '1.0-${bamboo.buildNumber}') {
              autoIncrement()
              applicableToBranches()
              variables 'var1', 'var2'
          }
          permissions {
          }
      }
  }
  ~~~
  {: title="DSL" }
  ~~~ yml
  plans:
    - key: SIMPLEPLAN
      name: my simple plan
      deploymentProjects:
        - id: 1
          name: DP1
          description: my deployment project
          useCustomPlanBranch: PLAN_BRANCH_NAME
          environments:
            - name: staging
              id: 1
              description: Staging env
            - name: prod
              id: 2
              description: Production env
          releaseVersioning:
             nextReleaseVersion: 1.0-${bamboo.buildNumber}
             autoIncrement: true
             applicableToBranches: true
             variables:
               - var1
               - var2
          permissions:
  ~~~
  {: title="YAML" }
---
A deployment project consists of a description, the name of the associated [plan branch](#branches)
(if not the default one), a number of [deployment environments](#environments) and release versioning information.

Note that the ID for both the deployment projects and the environments is optional and will be auto-generated if not
specified.