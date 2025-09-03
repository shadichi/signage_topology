# C3 — Services Architecture Diagram (Signage TV)

## هدف
نمای معماری در سطح سرویس های کلاینت: دانلود و کش محتوا، و پخش همزمان بر اساس زمان سرور. 

---

## اجزای اصلی
- Feature Home: Download Manager ،دریافت Schedule   
- Feature Video: کنترل پخش و همگام سازی با زمان سرور
- لایه ها: UI -> State -> Domain -> Data -> Remote/Local
- سرویس های بیرونی: Backend API، MQTT Broker، CDN

---

## Component Map per Feature

```mermaid
flowchart LR
  subgraph Home_Feature
    H_UI[Home Screen]
    H_State[Home Bloc]
    H_Use[UseCase - load schedule - download video - save to local db]
    H_Repo[Repository - load schedule - download video - save to local db]
    H_Remote[Remote - http client]
    H_Local[Local - cache files and prefs]
  end

  subgraph Video_Feature
    V_UI[Video Screen]
    V_State[Video Cubit - sync and playback]
    V_Use[UseCase - start stop seek]
    V_Repo[Repository - playback and control]
    V_MQTT[Remote - mqtt client]
    V_Local[Local - cached media files]
  end

  H_UI --> H_State --> H_Use --> H_Repo
  H_Repo --> H_Remote
  H_Repo --> H_Local

  V_UI --> V_State --> V_Use --> V_Repo
  V_Repo --> V_MQTT
  V_Repo --> V_Local

  %% Cross feature
  H_Local -. provides cached media .- V_Local




