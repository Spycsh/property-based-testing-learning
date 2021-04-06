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

* FORALL Macro

?FORALL(InstanceOfType, TypeGenerator, PropertyExpression).

can be translated in:

proper:forall(TypeGenerator, fun(InstanceOfType) -> PropertyExpression end).

* Generators

Eunit syntax
```
biggest_test() ->
  ?assert(5 =:= biggest([1, 2, 3, 4, 5])),
  ?assert(8 =:= biggest([3, 8, 7, -1])),
  ?assert(-5 =:= biggest([-10, -5, -901])),
  ?assert(0 =:= biggest([0])).
```

vs. PropEr(get a far better coverage of edge cases,including those we wouldn’t think of by ourselves)
```
prop_biggest() ->
  ?FORALL(List, list(integer()),
    begin
      biggest(List) =:= lists:last(lists:sort(List))
    end).
```

Of course we should not use lists:last and lists:sort anymore in implementation of the function biggest/1
