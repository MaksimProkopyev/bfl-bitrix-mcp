# BFL LeadGen — конвейер (Agent Builder)

Конвейер бесплатной/условно-бесплатной лидогенерации для бизнеса «банкротство физлиц (РФ)».
Путь данных: **Start → Set state (init) → Query Watcher → While (urls) → Traffic Harvester → Normalize → While (candidates) → Scrubber → If/Else → Generate Slots → Sale**  
Параллельный источник: **bfl_lead_intake_output → Normalize** (прямая связь в Sale удалена).

---

## 1) Назначение папки
- Хранит схемы, правила и чек-листы по настройке существующих узлов, без создания новых.
- Описывает идемпотентный порядок правок и прогон Preview.

---

## 2) Быстрый старт (идемпотентно)

1. **Set state (init)** — проверь, что заданы (не перетирать существующие):
   ```json
   {
     "dedup_hashes": {{ state.dedup_hashes || [] }},
     "last_seen_ts": {{ state.last_seen_ts || {} }},
     "seen_urls": {{ state.seen_urls || [] }},
     "metrics": {{ state.metrics || {"attempts":0,"replies":0,"booked":0,"duplicates":0,"pass":0,"source_stats":{}} }},
     "pass_threshold": {{ state.pass_threshold || 0.72 }}
   }
   ```
2. **Query Watcher** — синхронизируй частоту запусков с cron и проверь фильтры по ключевым словам.
3. **Traffic Harvester** — убедиcь, что парсер корректно извлекает `title`, `snippet`, `posted_at` и `region`.
4. **Normalize** — проверяй схему `schemas/batch_candidates.json`, прогоняй `npm run ci`.
5. **Scrubber** — смотри `schemas/scrubber_output.json`, дополняй `risk_flags` только whitelisted-значениями.
6. **Generate Slots → Sale** — подтверждай доступность CRM и корректность маппинга UTM-меток.

---

## 3) Чек-лист перед выкладкой
- [ ] Прогнан `npm run ci`.
- [ ] Обновлены шаблоны состояний и контактных полей.
- [ ] Зафиксированы изменения в `LeadGen/README.md` при необходимости.
- [ ] Отписано в канале поддержки об обновлении конвейера.
