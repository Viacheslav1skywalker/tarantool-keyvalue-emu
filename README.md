This is project-sample, which contain base functionality of the Tarantool 3.x.

Tarantool is not database, but application framework with built-in 2 databases types: memtx (in-memory) and vinyl (on-disk). https://www.tarantool.io/en/doc/latest/concepts/data_model/.

Current application emulate common Redis/Valkey API and allow to use it as cache or/and sessions storage for you simple project. You can use call functions like `CACHE:Set()`/`CACHE:Get()` with Tarantool's API (port 3301) or `SET`/`GET` with Redis API (port 6379). [Redis API is much faster than Tarantool's - 2x]

### List of files:

| file name            | description |
| ---                  | --- |
| `docker-compose.yml` | sample docker settings which run master with replica |
| `config.yaml`        | configs of the instance of the application (listener port, snapshot interval,.. plus structure of app-instances for master-replica cases )  |
| `instances.yml`      | list of instances for `tt`. Inside docker container it doesn't uses |
| `init.lua`           | start point of all functions |
| `init-cache.lua`     | class to work with cache-storage |
| `init-sessions.lua`  | class to work with sessions-storage  |
| `init-redis-emu.lua` | Redis/Valkey API handler |


### Replication
Steps to setup/uses:

1. setup schema in shared `config.yaml`
2. start instances
3. to add/remove instance you have to make changes in `config.yaml` and reload it for each instances via `require('config'):reload()` in `console` or `tt` (https://www.tarantool.io/en/doc/latest/how-to/replication/repl_bootstrap/)


### Useful links:
Not frequently updated Tarantool documentation:
https://www.tarantool.io/en/doc/latest/overview/

Lua's documentation (Tarantool uses LuaJit, which is equal to Lua 5.1):
https://www.lua.org/manual/5.1/

Lua in minutes:
https://learnxinyminutes.com/docs/ru-ru/lua-ru/

Lua performance tips: https://www.lua.org/gems/sample.pdf

Tarantool in Docker better learn from official source repository:
https://github.com/tarantool/tarantool/tree/master/docker