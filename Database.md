# Production
```
psql -h mfcmlms-postgres-0e3a534c1dea98d8.cmzemiutf0bp.ap-southeast-1.rds.amazonaws.com -U ro_user -p 5432 -d merchantlending
```

User and Password
```
User_ ro_user
7Lg3H$eY9#KBeFKQVRTh
```

# Development
aws 
```
aws --profile DeddyChandra@tvlk-mfc-stg ssm start-session --target i-0a2a2ef789388bc4b
```

```
psql -h mfcmlms-postgres-0259605d566873963.cmzemiutf0bp.ap-southeast-1.rds.amazonaws.com -U migration_user -p 5432 -d merchantlending
```

User and Password
```
migration_user
migration_user
```