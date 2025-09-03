# C2 — Services Dependency Diagram (Signage)

## هدف
نمای کلی از لایه‌های اپ TV (Flutter)، ماژول‌ها/فچرها، پکیج‌های کلیدی، و وابستگی به سرویس‌های بیرونی (API، MQTT، CDN).

---

## لایه‌ها و وابستگی‌ها (High-level)
> جهت فلش یعنی «وابستگی». UI به State وابسته است، State به Domain، Domain به Data، و Data به منابع Remote/Local.

## 🔗 Services Dependency Diagram

```mermaid
flowchart TB
  subgraph App[Flutter TV App]
    UI[UI / Screens]
    STATE[State Management - Bloc or Cubit]
    DOMAIN[Domain - Entities and UseCases]
    DATA[Data Layer - Repositories]
    RMT[Remote Sources - HTTP and MQTT]
    LOC[Local Cache - Files or SharedPrefs]
  end

  UI --> STATE
  STATE --> DOMAIN
  DOMAIN --> DATA
  DATA --> RMT
  DATA --> LOC

  RMT --> API[(Backend API)]
  RMT --> MQTT[(MQTT Broker)]
  LOC --> FILES[(Video Files Cache)]
```