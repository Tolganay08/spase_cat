# SPACE CAT: Defend Miau-Prime (Unity 6 — 2D Neon Space Arcade + Задание 3)

Полноценная учебная 2D-игра в жанре **Space Arcade Shooter** для **Unity 6** с главным героем **Captain Meow** (рыжий кот-космонавт), кораблём **Star Paws**, планетой **Miau-Prime**, **3 уровнями**, боссом **MegaBot**, а также полным выполнением **Задания 3 («От запуска до победы»)**.

---

## 1. Как открыть и запустить игру на MacBook и Windows

### На MacBook (macOS):
1. На вашем Рабочем столе уже создана готовая папка проекта **`Space_Cat`** (и архив **`Space_Cat_Unity_Project.zip`**).
2. Откройте **Unity Hub** ➔ нажмите кнопку **`Add` ➔ `Add project from disk`**.
3. Выберите папку **`Space_Cat`** на Рабочем столе и откройте проект в **Unity 6** (`6000.x`).
4. В верхнем меню Unity нажмите **`Space Cat` ➔ `2. Запустить игру (▶ Play SPACE CAT)`** (или просто нажмите кнопку **▶ Play** сверху по центру).

### На Windows:
1. Распакуйте архив **`Space_Cat_Unity_Project.zip`** в любую папку (например, `C:\Games\Space_Cat`).
2. Откройте **Unity Hub** ➔ **`Add` ➔ `Add project from disk`** ➔ выберите папку **`Space_Cat`**.
3. Откройте сцену `Assets/Scenes/SampleScene.unity` (или `Assets/Scenes/Boot.unity`) и нажмите **▶ Play**.

---

## 2. Управление в игре (Gameplay Controls)

* **`A` / `D`** или **`Стрелки Влево / Вправо`** — плавное движение корабля влево и вправо.
* **`W` / `S`** или **`Стрелки Вверх / Вниз`** — маневровые двигатели.
* **`SPACE` (Пробел)** или **Левая кнопка мыши (ЛКМ)** — стрельба неоновыми лазерами.
* **`ESC`** — меню паузы (`Pause Menu`).
* **`R`** — быстрый перезапуск уровня (`Restart`).
* **Любая клавиша / клик мыши** во время катсцены — пропуск вступительной катсцены (`Cutscene`).

---

## 3. Что реализовано для сдачи «Задания 3» (Чек-лист на 10/10 баллов)

1. **Экран загрузки (`Assets/Scenes/Boot.unity` + `Assets/Scripts/BootLoader.cs`)**:
   * При запуске появляется экран с логотипом **SPACE CAT** и полосой загрузки **`ProgressBar`** (`Slider` без круглого бегунка `Handle`, `Interactable = false`, `Value = 0..1`).
   * Корутина `IEnumerator Start()` использует `SceneManager.LoadSceneAsync`, `op.allowSceneActivation = false`, `op.progress / 0.9f` и `minDisplayTime = 2.2f`.
2. **Вступительная катсцена с миссией (`Assets/Scenes/Intro.unity` + `Assets/Scripts/Cutscene.cs` + `Assets/Scripts/TypewriterText.cs`)**:
   * **Вариант А (Слайды с плавным переходом через `CanvasGroup` и эффектом печатной машинки `TypewriterText`)**.
   * Состоит из 3 слайдов (`Slide1`, `Slide2`, `Slide3`), пропускается по любой клавише или клику мыши.
   * **Текст миссии (для сдачи в сообщении преподавателю)**:
     > *«Ты — Капитан Мяу за штурвалом корабля Star Paws. Враждебные дроны Robo-X и босс MegaBot атакуют планету Miau-Prime метеоритами. Уничтожь 10 метеоритов на 1-м уровне (15 роботов на 2-м и босса MegaBot с 20 HP на 3-м), чтобы спасти планету!»*
   * **Предложение о выбранном варианте катсцены**:
     > *«Мы выбрали Вариант А (катсцена со слайдами CanvasGroup и эффектом печатной машинки TypewriterText), так как она наглядно показывает предысторию планеты Miau-Prime и точную боевую задачу перед стартом каждого уровня.»*
3. **Условие победы и прогресс на экране (`Assets/Scripts/Managers/GameManager.cs`, `Collectible.cs`, `ExitZone.cs`, `SurvivalGoal.cs`)**:
   * Сверху по центру экрана отображается прогресс **`GoalText`** в формате **`3 / 10`** (на 1-м уровне нужно сбить ровно 10 метеоритов, на 2-м — 15 роботов, на 3-м — победить босса MegaBot с 20 HP).
4. **Экран победы (`VictoryPanel`)**:
   * Отображает время прохождения (`Время: X.X с`), итоговые очки (`Очки: Y`), заработанные монеты и работающие кнопки перезапуска (`REPLAY`), следующего уровня (`NEXT LEVEL`) и выхода в меню (`MAIN MENU`).
   * После победы над боссом MegaBot на 3-м уровне открывается финальный экран **`PLANET SAVED! YOU ARE A HERO!`** с анимацией Капитана Мяу.

---

## 4. Архитектура папок и скриптов (`Assets/`)

* **`Assets/Scenes/`**: `Boot.unity`, `MainMenu.unity`, `Intro.unity`, `GameScene.unity`, `SampleScene.unity`.
* **`Assets/Scripts/`**:
  * `BootLoader.cs`, `Cutscene.cs`, `TypewriterText.cs`, `Collectible.cs`, `ExitZone.cs`, `SurvivalGoal.cs` (скрипты по методичке Задания 3).
  * `Managers/`: `GameManager.cs`, `LevelManager.cs`, `UIManager.cs`, `ProfileManager.cs`, `AuthManager.cs`, `ShopManager.cs`, `LeaderboardManager.cs`, `SaveManager.cs`, `AudioManager.cs`, `SettingsManager.cs`.
  * `Player/`: `PlayerController.cs`, `WeaponController.cs`, `Bullet.cs`.
  * `Enemies/`: `EnemyController.cs`, `EnemySpawner.cs`, `BossController.cs`.
  * `UI/`: `UIButtonFX.cs`, `FloatingTextFX.cs`, `StarfieldAnimator.cs`.
  * `Data/`: `GameDataModels.cs`, `LocalizationData.cs`, `ProceduralSprites.cs`.
  * `Editor/`: `SpaceCatProjectSetup.cs`.
* **`Assets/Sprites/`**:
  * `Characters/`: 5 аватаров котов (`CatAvatar_1.png`..`5.png`) и `CaptainMeow_Hero.png`.
  * `Spaceships/`: 4 корабля (`Ship_StarPaws.png`, `Ship_NeonKitty.png`, `Ship_GalaxyHunter.png`, `Ship_CosmicLegend.png`).
  * `Enemies/`: `Enemy_Meteor.png`, `Enemy_RoboX.png`, `Boss_MegaBot.png`.
  * `Backgrounds/`: 3 фона уровней и планета `Planet_MiauPrime.png`.
* **`Assets/Audio/`**: WAV-звуки лазеров, взрывов, кнопок, бонусов и фанфары победы.
# spase_cat
