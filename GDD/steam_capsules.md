# Hold the Resort — Steam Capsules Pack (Store + Library)

Версия 1.2 · 21.10.2026 · стиль не входит, подставляется пайплайном в `[STYLE]`
Источники: `concept_v3.1.md`, `art_list_demo.md`, `staff_enemies_matrix.md`, `demo_plan.md`
**Концепт: «Домовой выносит фойе»** — день, локация 1, босс демо.

> ⚑ **Решения, принятые за тебя** — проверь:
> 1. В каждый промпт добавлен плейсхолдер `[STYLE]` под твою мастер-строку стиля.
> 2. Арт генерируется **без текста**, вывески пустые (иначе пришлось бы делать 3 языковые версии арта). Логотип собирается отдельно в редакторе.
> 3. **DE:** основное название оставлено английским, локализован только подзаголовок — *Gäste gegen Geister*.
> 4. **RU:** логотип = **«Путёвка в Лихо»**, подзаголовок опционально — «Гости против нечисти». Альтернатива: *Hold the Resort* + «Гости против духов».
> 5. Описания персонажей взяты из `art_list_demo.md` (переведены на английский); на капсуле только персонажи демо.
> 6. Броня-атрибуты нечисти не используются — в демо их нет.
> 7. В негатив добавлены политические символы (серп и молот, звёзды, флаги, вожди) и оружие.
> 8. Концепты A и C удалены из пакета.

---

## 1. Спецификации

| Ассет | Размер | Логотип | Источник арта |
|---|---|---|---|
| Header Capsule | 920×430 | да | Wide (кроп) |
| Small Capsule | 462×174 | да, занимает бо́льшую часть | отдельный промпт |
| Main Capsule | 1232×706 | да | Wide (кроп) |
| Vertical Capsule | 748×896 | да | Vertical |
| Library Capsule | 600×900 | да | Vertical (кроп) |
| Library Header | 920×430 | да | = Header Capsule |
| Library Hero | 3840×1240 | **нет, без текста** | Wide (мастер) |
| Library Logo | 1280×720, PNG с прозрачностью | — | логотип; вписать по ширине 1280 **или** высоте 720 |

Не покрыто: скриншоты, Page Background, иконка сообщества 184×184, иконка клиента.

**Правила Steam (ключевое):**
- На капсулах только арт + название/логотип. Никаких наград, цитат из обзоров, скидок, «Coming Soon», «Demo», «Next Fest».
- Library Hero — без текста и логотипа; логотип Steam накладывает сам (позиция настраивается). Фокус — в центральной трети, нижний левый угол не загружать.
- Локализованные капсулы загружаются отдельно по языкам (EN по умолчанию, DE и RU — локальные версии).
- Арт капсулы должен соответствовать игре — те же дизайны персонажей, что в билде.
- AI-арт → обязательно указать в Content Survey (раскрытие AI-генерации).

---

## 2. Пайплайн

1. **Тест:** Wide + Vertical + Small, по 2–4 варианта генерации. Проверка: уменьшить до 231×87 (половина Small) и 184 px по ширине — Домовой с креслом читается?
2. **Финал:** лучший вариант — генерация в максимальном разрешении → апскейл → аутпейнт Wide до 3.1:1 для Hero.
3. **Кропы:** Wide → Hero / Main / Header; Vertical → Vertical / Library Capsule.
4. **Логотип:** эмблема (промпт §5) + шрифт вручную → 3 языка × все форматы.
5. **QA:** проверка на тёмном фоне Steam (`#1b2838`), в градациях серого, на 25% масштабе; сверка персонажей с игровыми спрайтами.
6. **Экспорт и загрузка:** EN по умолчанию, DE / RU локальными версиями.

**Соотношения для генератора** (если нет точного — ближайшее + кроп/аутпейнт):
Wide 3:1 (или 21:9) · Main 16:9 · Header 2:1 · Vertical 5:6 (или 4:5) · Library Capsule 2:3 · Small 21:9 → кроп 2.65:1.

**Ракурс:** игровые спрайты — как в PvZ 1 (спереди чуть сверху). Капсула — key art, ракурс свободнее, но пропорции персонажей те же: Домовой ≈ вдвое выше человека, злыдень ростом с кошку.

---

## 3. Персонажи (вставки для промптов)

Использовать одинаковые формулировки во всех промптах — для консистентности.

```
SETTING     = the grounds of a Soviet tourist complex in Suzdal, 1973: wrought-iron gates, an asphalt path with curbs and lawns leading to a two-storey light-brick building with two wide glass doors, a small newspaper-and-souvenir kiosk with a blank sign, a soda water vending machine, a round flower bed with marigolds and silver wormwood; beyond the fence, white-stone churches with onion domes and a forest edge

# Гости
GUEST       = a man in a short-sleeve polo shirt, trousers and sandals with socks, a camera on a strap
GUEST_W     = a woman in a polka-dot cotton dress and a panama hat, with a handbag
GRANNY      = an elderly woman in a headscarf and cardigan holding a string bag

# Персонал
PORTER      = an elderly moustached porter in a braided uniform jacket and peaked cap, holding a suitcase overhead ready to throw
ADMIN       = a middle-aged woman with a tall hairdo, a strict suit and glasses, swinging a bunch of room keys
DRIVER      = a sturdy bus driver in a cap and work jacket, a big wrench in hand
MAID        = a young maid in a uniform dress, white apron and headscarf, swinging a mop, a bucket at her feet

# Нечисть
ZLYDNI      = Zlydni, small thin hunched creatures the size of a cat, long arms, big greedy eyes, grey fur, tiptoeing
KIKIMORA    = Kikimora, a small hunched old-woman spirit with a beak-like nose and thin legs, in rags, holding a ball of tangled yarn
LIKHOMANKA  = Likhomanka, a thin pale maiden in a long white shirt, loose hair, blue lips, shivering, light frost around her
ANCHUTKA    = Anchutka, a little imp with small horns, a tail and hooves, running at full speed with a string bag of stolen tools — a mop and keys sticking out
DOMOVOY     = Domovoy, a short stocky old man covered in fur with a long beard, bast shoes and a belted peasant shirt, carrying a lobby armchair on his back, a bunch of keys dangling from his pocket, twice the height of a human
```

**Негатив (общий для всех):**
```
text, letters, words, numbers, typography, writing on signs, logo, watermark, signature, UI, HUD, frame, border, political symbols, flags, hammer and sickle, red stars, portraits of leaders, guns, modern clothing, smartphones, modern cars, gore, blood, cropped heads, extra limbs, cluttered background
```

---

## 4. Промпты — «Домовой выносит фойе» (Day Shift)

*Хук: Домовой тащит кресло из фойе, нечисть бьёт по всем трём звеньям (гости, объекты, персонал), персонал отбивается. Точно совпадает с демо.*

**Wide** (Hero / Main / Header · 3:1)
```
Wide sunny summer day scene at SETTING. Center: DOMOVOY stomping out of the glass doors of the brick building, the lobby armchair on his back, keys jingling. Staff fight back around him: MAID smacking him with her mop, PORTER mid-throw with a suitcase, ADMIN hurling keys, DRIVER charging in with his wrench. Around the courtyard the three threats at once: a swarm of ZLYDNI clinging to the kiosk (left), LIKHOMANKA breathing frost on GUEST, who shivers and drops his camera, ANCHUTKA dashing away with a string bag of stolen tools (right), KIKIMORA tangling yarn around the soda vending machine. GUEST_W and GRANNY watching in shock; GRANNY shooing a zlydni with her string bag. Onion domes and forest beyond the fence. Bright, chaotic but readable, focal action in the central third. [STYLE]
```

**Main/Header** (16:9 / 2:1 — если кроп из Wide не работает)
```
Dynamic sunny day shot at SETTING. Center: DOMOVOY carrying the lobby armchair out of the glass doors. MAID swings her mop at him from the left, PORTER throws a suitcase from the right. Foreground: a swarm of ZLYDNI clinging to the kiosk, ANCHUTKA running off with stolen tools. Background: brick building, fence, onion domes. Upper-left area kept as simple summer sky for a title. Big readable shapes, clear diagonal motion. [STYLE]
```

**Vertical** (Vertical / Library Capsule · 5:6 и 2:3)
```
Vertical composition, sunny day at SETTING. Center: DOMOVOY towering in the doorway of the brick building, the lobby armchair on his back. Below him MAID and PORTER fight back with mop and suitcase, ADMIN throwing keys from the side. Bottom: ZLYDNI swarming the flower bed, GUEST shivering beside LIKHOMANKA. Onion domes behind the roof. Top 25% kept as clean sky for a title. [STYLE]
```

**Small** (21:9 → 462×174)
```
Minimal horizontal composition. Right third: DOMOVOY from the chest up, furry face and long beard, the lobby armchair on his back, a mop smacking him on the head from off-frame. Left two thirds: plain summer-sky gradient, empty, for a large title. Big shapes, high contrast, readable at thumbnail size. [STYLE]
```

---

## 5. Логотип

**Тексты:**

| Язык | Строка 1 (крупно) | Строка 2 (подзаголовок) |
|---|---|---|
| EN | HOLD THE RESORT | Guests vs. Ghosts |
| DE | HOLD THE RESORT | Gäste gegen Geister |
| RU | ПУТЁВКА В ЛИХО | Гости против нечисти *(опц.)* |

- Вёрстка: 2 строки, подзаголовок ≤ 60% ширины заголовка. DE — самый длинный подзаголовок, под него и рассчитывать макет.
- Нужен шрифт с полной кириллицей и Ä/ä — проверить до выбора.
- Размер логотипа: Header ~50% ширины · Main ~40% · Vertical / Library Capsule ~75% · Small — максимум, вписать по высоте/ширине с полем ~8%.
- Отдельная **короткая версия** для Small: только строка 1 (подзаголовок там не читается).

**Промпты эмблем** (без текста, под вписывание букв):

*L1 — Вымпел*
```
A 1970s Soviet souvenir pennant (triangular felt pennant with tassel fringe), large blank central area for lettering, a ZLYDNI peeking over the top edge with greedy eyes, ANCHUTKA hanging from the tassel with a string bag. Centered, isolated on a plain flat background for easy cutout. [STYLE]
```

*L2 — Табличка на ресепшен*
```
A vintage wooden reception desk sign on a small stand, blank wide panel for lettering, a bunch of room keys with pear-shaped wooden tags hanging from one corner, KIKIMORA's thin hand with a strand of yarn curling around the other. Centered, isolated on a plain flat background for easy cutout. [STYLE]
```

---

## 6. Чек-лист перед загрузкой

- [ ] Домовой с креслом читается на 25% и 184 px
- [ ] Все 8 ассетов × 3 языка (Hero — один на все языки, без текста)
- [ ] Логотип читается на Small Capsule
- [ ] На капсулах нет ничего, кроме арта и названия
- [ ] Персонажи совпадают с игровыми спрайтами (арт-лист)
- [ ] Library Logo — PNG с прозрачностью, вписан в 1280×720
- [ ] AI-генерация отмечена в Content Survey
- [ ] Название в Steamworks совпадает с логотипом на локализованной капсуле
