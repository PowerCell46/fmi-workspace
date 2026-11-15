Endpoints:


GET /api/v1/current-walking-routes-state {lat, lon, radius=defaultValue} URL params

GET /api/v1/hazards-notifications {lat, lon, radius=defaultValue} URL params
GET /api/v1/alternative-routes {lat, lon, destLat, destLon} URL params

---
## Register an user

POST 
/api/v1/users/register
```
username: string;
password: string;
```

---
### An admin changing the role of an user
PATCH 
/api/v1/users/assign-role
```
username: string;
role: Role
```