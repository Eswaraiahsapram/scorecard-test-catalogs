# Scorecard test catalogs

Catalog-only examples for exercising the scorecard plugin in a cluster. Annotations follow the local examples in `rhdh-plugins/workspaces/scorecard/examples`.

Register this location:

```yaml
catalog:
  locations:
    - type: url
      target: https://github.com/Eswaraiahsapram/scorecard-test-catalogs/blob/main/catalog-info.yaml
      rules:
        - allow: [Component, Group, Location]
```

You can also paste `https://github.com/Eswaraiahsapram/scorecard-test-catalogs` into the catalog import page. The import looks for `catalog-info.yaml`.

## Examples

| Entity | What it exercises |
| --- | --- |
| `component:default/scorecard-rhdh-plugins` | GitHub open PRs, Jira open issues, Dependabot, SonarQube, OpenSSF, code coverage, file checks |
| `component:default/scorecard-rhdh` | A second GitHub and Jira service, including `jira/label`, so aggregation min/max/sum can differ |
| `component:default/scorecard-catalog-with-title` | Catalog title check passes |
| `component:default/scorecard-catalog-without-title` | Catalog title check fails |
| `component:default/scorecard-dora` | DORA metrics (`scorecard.io/dora`) |

Homepage KPIs only include entities owned by the signed-in user. These components are owned by `group:development/guests` and `group:default/red-hat`. Add your cluster user to the matching group, or change `spec.owner`, if those KPIs stay empty. The entity Scorecard tab still works either way.

`jira/project-key: RHIDP` and `jira/incident-project-key: RSPT` match the local scorecard config. Point them at projects that exist in the cluster Jira before expecting Jira and DORA numbers.

If `group:development/guests` or `group:default/red-hat` are already in the catalog, remove `./org.yaml` from `catalog-info.yaml` so the location does not register a duplicate.
