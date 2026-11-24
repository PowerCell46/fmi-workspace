
---
### Endpoint where an admin can alter the role of the users
It's important to discuss here whether the relationship is ManytoOne between User and Role or Many to many

PATCH request
```json
{
    id: "String",
    role: "Role"
}
```

response format:
either successful operation or not (error)