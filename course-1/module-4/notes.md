# Camera Geometry & Epipolar Geometry: Module Notes

Конспект модуля по computer vision: проекция 3D → 2D, параметры камеры и эпиполярная геометрия.

## 1. Perspective projection

- Перспективная проекция переводит 3D-точки в координаты на плоскости изображения.
- Вычисления ведутся в **homogeneous coordinates**: так проекцию (нелинейную в обычных координатах) можно записать матричным умножением.
- **Offset** (смещение principal point) сдвигает объект в плоскости изображения, но не меняет масштаб, поворот или глубину.

## 2. Intrinsic и extrinsic параметры

| | Intrinsic matrix K | Extrinsic matrix [R \| t] |
|---|---|---|
| Что описывает | Внутренние свойства камеры | Положение и ориентацию камеры в мире |
| Из чего состоит | Focal length, optical center (principal point), (skew) | Rotation R и translation t |
| Назначение | Camera coordinates → pixel coordinates | World coordinates → camera coordinates |

- Elements of K: **focal length** и **optical center**. Translation vectors и distortion coefficients в K не входят.
- **Translation matrix** меняет начало системы координат (origin), **rotation matrix** поворачивает камеру. Вместе они позволяют переставлять и переориентировать камеру в 3D-сцене.

## 3. Projection matrix

```
P = K [R | t]
x = P X
```

Назначение: преобразовать 3D-координаты в 2D-координаты для отображения на плоскости изображения. К цвету, освещению и текстурам отношения не имеет.

## 4. Surface normal

Нормаль к поверхности считается через **cross product** двух векторов, лежащих в плоскости поверхности.

## 5. Epipolar geometry

Геометрия двух видов одной сцены.

**Компоненты:**
- **Baseline**: линия, соединяющая центры двух камер.
- **Epipoles**: точки, в которых baseline пересекает плоскости изображений (проекция центра одной камеры на изображение другой).
- **Epipolar plane**: плоскость, проходящая через baseline и 3D-точку.
- **Epipolar lines**: пересечение epipolar plane с плоскостью изображения. Все epipolar lines сходятся в epipole.

**Зачем нужна:**
- Упрощает **correspondence problem**: соответствие точке в первом изображении ищется не по всему второму кадру, а только вдоль epipolar line (поиск 2D → 1D).
- Задаёт связь между двумя видами, то есть между плоскостями изображений двух камер.
- К color, resolution, focus и time sync отношения не имеет.

## 6. Essential и Fundamental matrix

**Epipolar constraint:**

```
x'ᵀ E x = 0      (в нормализованных координатах, K известна)
x'ᵀ F x = 0      (в пиксельных координатах)
```

```
E = [t]ₓ R
F = K'⁻ᵀ E K⁻¹
```

| | Essential matrix E | Fundamental matrix F |
|---|---|---|
| Кодирует | Relative rotation и translation между камерами | Epipolar geometry между двумя видами в пикселях |
| Intrinsics | Предполагаются известными | Не требуются |
| Ключевой смысл | Relative orientation и position камер | Связь между пиксельными координатами двух видов |

**Что участвует в выводе epipolar constraint:** relative camera orientation, camera intrinsic parameters, matrix transformations (rotation, translation, cross-product matrix). Для вывода используются матричные операции и тригонометрия.

**Translation T между камерами** определяется положением камер и расстоянием между ними (baseline). Resolution и aperture на него не влияют.

## Key takeaways

1. K описывает камеру, [R | t] описывает её положение; вместе они дают P = K[R | t].
2. Epipolar geometry сводит поиск соответствий к поиску вдоль линии.
3. E работает с нормализованными координатами (нужна K), F работает напрямую с пикселями.
