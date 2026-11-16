Endpoints:

Получават информация за текущото състояние на пешеходните маршрути
GET /api/v1/current-walking-routes-state {lat, lon, radius=defaultValue} URL params

Получават предупреждения при опасни условия
GET /api/v1/hazards-notifications {lat, lon, radius=defaultValue} URL params

Виждат алтернативни маршрути с по-безопасни условия
GET /api/v1/alternative-routes {lat, lon, destLat, destLon} URL params
