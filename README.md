# property-based-testing-learning
```
$ rebar3 new lib pbt
$ cd pbt
```
In rebar.config
```
%% the plugin itself
{project_plugins, [rebar3_proper]}.
%% The PropEr dependency is still required to compile the test cases,
%% but only as a test dependency
{profiles,
[{test, [
{erl_opts, [nowarn_export_all]},
{deps, [proper]}
]}
]}.
```

```
$ rebar3 help proper
$ rebar3 new proper foundations
$ rebar3 proper -n 10000
```
