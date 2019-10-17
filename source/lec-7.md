# Лекция 7 (от 14.10)

### __Методы поиска доверительных интервалов__

#### 1. Метод центральной функции
Пусть $G(X, \theta)$ — функция, распределение которой известно и не зависит от $\theta$ (_центральная функция_). Возьмем $\alpha_1, \alpha_2 \in (0, 1)$ т. ч. $\alpha_2 -\alpha_1 = \alpha$ и $g_j$ — $\alpha_j$-квантиль распределения $G(X, \theta)$. Тогда $S(X) = \{\theta \in \Theta \vert g_1 \leqslant G(X, \theta) \leqslant g_2 \}$ — доверительная область уровня доверия $\alpha$.  
Действительно, $P_\theta(\theta \in S(X)) = P_\theta(g_1 \leqslant G(X, \theta) \leqslant g_2) = \alpha_2 - \alpha_1 = \alpha.$  

__Пример:__ $X_1, \dots, X_n \sim \mathcal{N}(\theta, \sigma^2)$, $\sigma$ известно. Построить точные доверительные интервалы для $\theta$.  

$\triangle \quad$ Заметим, что $X_i - \theta \sim \mathcal{N}(0, \sigma^2)$, следовательно, $\overline{X} - \theta \sim \mathcal{N}(0, \frac{\sigma^2}{n}).$  
$G(X, \theta) = \sqrt{n}\dfrac{\overline{X} - \theta}{\sigma} \sim \mathcal{N}(0, 1)$ — центральная функция. Будем обозначать через $z_p$ $\ p$-квантили распределения $\mathcal{N}(0, 1)$. Тогда 
$$ P_\theta\left(-z_{\frac{1+\alpha}{2}} \leqslant\sqrt{n}\dfrac{\overline{X} - \theta}{\sigma} \leqslant  z_{\frac{1+\alpha}{2}} \right) = \alpha \implies P_\theta \left(\overline{X} - \dfrac{z_{\frac{1+\alpha}{2}}  \sigma}{\sqrt{n}} \leqslant \theta \leqslant \overline{X} + \dfrac{z_{\frac{1+\alpha}{2}}  \sigma}{\sqrt{n}} \right) = \alpha.
$$

__Ответ:__ $\left(\overline{X} \pm \dfrac{z_{\frac{1+\alpha}{2}} \sigma}{\sqrt{n}}\right)$.

Пусть $\alpha = 0.95 \implies z_{\frac{1+\alpha}{2}} = z_{0.975} \approx 1.96 \approx 2$. $n = 100, \overline{x} = 5, \sigma=1$. Тогда реализация интервала $(5 \pm 2/10) = (4.8, 5.2).$

#### 2. Асимптотические доверительные интервалы
>__Определение:__ Пусть $X = (X_1, X_2, \dots)$ — выборка неограниченного размера из распределения $P \in \{P_\theta \vert \theta \in \Theta\}$. Последовательность пар статистик $(T_1^{(n)}(X_1, \dots, X_n), T_2^{(n)}(X_1, \dots, X_n))$ называется _асимптотическим доверительным интервалом_ уровня доверия $\alpha$, если  
>$$\forall \theta \in \Theta \liminf_{n \to\infty} P_\theta(T_1^{(n)}(X_1, \dots, X_n) \leqslant \theta \leqslant T_2^{(n)}(X_1, \dots, X_n)) \geqslant \alpha. $$ 
> Он называется _точным_, если 
> $$\forall \theta \in \Theta \lim_{n\to\infty} P_\theta(T_1^{(n)}\leqslant \theta \leqslant T_2^{(n)}) = \alpha.$$

__Метод построения асимптотического доверительного интервала:__
1. Пусть $\widehat{\theta}$ — а.н.о $\theta$ с асимпт. дисперсией $\sigma^2(\theta)$.
   $$\sqrt{n}(\widehat{\theta} - \theta) \xrightarrow{d_\theta} \mathcal{N}(0, \sigma^2(\theta)). $$
2. Поделим все на $\sigma(\theta)$:
   $$\dfrac{\sqrt{n}(\widehat{\theta} - \theta)}{\sigma(\theta)} \xrightarrow{d_\theta} \mathcal{N}(0, 1). $$
   Из теоремы Александрова
   $$ P_\theta\left(\dfrac{\sqrt{n}(\widehat{\theta} - \theta)}{\sigma(\theta)} \leqslant z_{\frac{1+\alpha}{2}}\right) \rightarrow \alpha. $$
   Проблема: $\sigma(\theta)$ может плохо зависеть от $\theta$.
3. Пусть $\widehat{\sigma}$ — состоятельная оценка $\sigma(\theta)$. Тогда
    $$ \sqrt{n}\dfrac{\widehat{\theta} - \theta}{\widehat{\sigma}} = \underbrace{\sqrt{n}\dfrac{\widehat{\theta} - \theta}{\sigma(\theta)}}_{\xrightarrow{d_\theta} \mathcal{N}(0,1)} \cdot \underbrace{\dfrac{\sigma(\theta)}{\widehat{\sigma}}}_{\xrightarrow{P_\theta} 1 \text{ (th о насл. сх-тей)}}. $$

    По лемме Слуцкого $\sqrt{n}\dfrac{\widehat{\theta} - \theta}{\widehat{\sigma}} \xrightarrow{d_\theta} \mathcal{N}(0, 1)$.
4. $P_\theta\left(\dfrac{\sqrt{n}(\widehat{\theta} - \theta)}{\widehat{\sigma}} \leqslant z_{\frac{1+\alpha}{2}}\right) \rightarrow \alpha.$ Получаем интервал $\left(\widehat{\theta} \pm \dfrac{z_{\frac{1+\alpha}{2}} \widehat{\sigma}}{\sqrt{n}} \right)$ — точный асимптотический доверительный интервал уровная доверия $\alpha$.
5. Откуда взять $\widehat{\sigma}$?  
   Если $\sigma(\theta)$ непрерывна, то по теореме о наследовании сходимостей $\widehat{\sigma} = \sigma(\widehat{\theta})$ — состоятельная оценка $\sigma(\theta)$.

__Пример:__  
1. $X_1, \dots, X_n \sim \mathcal{N}(\theta, \sigma^2), \ \sigma$ неизвестна. Построить асимптотический доверительный интервал уровня доверия $\alpha$ для $\theta$.
$\triangle \quad \overline{X}$ — а.н.о $\theta$ c асимпт. дисперсией $\sigma^2$. $S$ — состоятельная оценка $\theta$. Получаем интервал $\left(\overline{X} \pm z_{\frac{1+\alpha}{2}}\dfrac{S}{\sqrt{n}}\right). \quad \square$ 
2. $X_1, \dots, X_n \sim Pois(\theta)$. Построить асимптотический доверительный интервал уровня доверия $\alpha$ для $\theta$.  
$\triangle \quad \overline{X}$ — а.н.о $\theta$ c асимпт. дисперсией $\sigma^2(\theta) = \theta$. $\sqrt{\overline{X}}$ — состоятельная оценка $\sigma(\theta) = \sqrt{\theta}.$ Получаем интервал $\left(\overline{X} \pm z_{\frac{1+\alpha}{2}}\sqrt{\dfrac{\overline{X}}{n}}\right). \quad \square$ 

__Замечание:__ При $n=30$ условие ЦПТ применимо с хорошей точностью. Поэтому при $n \geqslant 30$ имеет смысл пользоваться асимптотическими доверительными интервалами.

### __3.2. Точые доверительные интервалы в нормальной модели__

Пусть $X = (X_1, \dots, X_n) \sim \mathcal{N}(a, \sigma^2).$
#### 1. Интервал для $a$, если $\sigma$ известна
Уже получили: $\left(\overline{X} \pm z_{\frac{1+\alpha}{2}}\dfrac{S}{\sqrt{n}}\right)$.

#### 2. Интервал для $\sigma$, если $a$ известно  

$\dfrac{X_i - \theta}{\sigma} \sim \mathcal{N}(0, 1)$

$G(X, \theta) = \sum\limits_{i=1}^n\left(\dfrac{X_i - a}{\sigma}\right)^2 \sim \chi^2_n$ — центральная функция _(распределение хи-квадрат с $n$ степенями свободы)_
$$ P_\theta\left(\chi^2_{n, \frac{1-\alpha}{2}} \leqslant \dfrac{1}{\sigma^2}\sum_{i=1}^n (X_i - a)^2 \leqslant \chi^2_{n, \frac{1+\alpha}{2}} \right) = \alpha $$

Получаем интервал $\left(\sqrt{\dfrac{\sum(X_i - a)^2}{\chi^2_{n, \frac{1+\alpha}{2}}}}, \sqrt{\dfrac{\sum(X_i - a)^2}{\chi^2_{n, \frac{1-\alpha}{2}}}}\right)$.

#### 3. Интервал для $a$, если $\sigma$ неизвестна 
>__Теорема:__ Пусть $X=(X_1, \dots, X_n) \sim \mathcal{N}(a, \sigma^2)$. Тогда:
>1. Статистики $\overline{X}$ и $S^2$ независимы
>2. $\dfrac{nS^2}{\sigma^2} \sim \chi_{n-1}^2$
>3. $\sqrt{n-1} \dfrac{\overline{X} - a}{S} \sim T_{n-1}$ — _распределение Стьюдента с $n-1$ степенями свободы_.

$\triangle \quad$ 1), 2) — позже  
3) $\sqrt{n} \dfrac{\overline{X} - a}{\sigma} \sim \mathcal{N}(0, 1); \  \dfrac{nS^2}{\sigma^2} \sim \chi^2_{n-1}$

Свойство распределения Стьюдента: если $\xi \sim \mathcal{N}(0, 1), \eta \sim \chi^2_k$ — независимые с.в., то $\zeta = \frac{\xi}{\sqrt{\eta / k}} \sim T_k$. Следовательно:

$$ \dfrac{\sqrt{n}\dfrac{\overline{X} - a}{\sigma}}{\sqrt{\dfrac{nS^2}{\sigma^2} \cdot \dfrac{1}{n-1}}} = \sqrt{n-1}\dfrac{\overline{X} - a}{S} \sim T_{n-1}. \quad \square $$

$G(X, \theta) = \sqrt{n-1}\dfrac{\overline{X} - \theta}{S}$ — центральная функция.

Получаем интервал $\left(\overline{X} \pm T_{n-1, \frac{1 + \alpha}{2}} \dfrac{S}{\sqrt{n-1}}\right)$.  
__Замечание__: При больших $n$ интервал почти совпадает с интервалом из пункта 1.

#### 4. Интервал для $\sigma$, если $a$ неизвестно

$G(X, \sigma) = \dfrac{nS^2}{\sigma^2} \sim \chi^2_{n-1}$ — центральная функция. Аналогично п.2 получаем интервал $\left(\sqrt{\dfrac{nS^2}{\chi^2_{n, \frac{1+\alpha}{2}}}}, \sqrt{\dfrac{nS^2}{\chi^2_{n, \frac{1-\alpha}{2}}}}\right)$.

>__Теорема (о разложении гауссовского вектора):__
Пусть $\xi = (\xi_1, \dots, \xi_n) \sim \mathcal{N} (a, \sigma^2 I_n)$,  $\R^n = \mathcal{L}_1 \oplus \dots \oplus \mathcal{L}_k$ — разложение в прямую сумму ортогональных подпространств, $\eta_j = \operatorname{proj}_{\mathcal{L}_j} \xi$ — проекция на $\mathcal{L}_j$. Тогда:
>1. $\eta_1, \dots, \eta_k$ независимы в совокупности;
>2. $E\eta_j = \operatorname{proj}_{\mathcal{L}_j} a$;
>3. $\frac{1}{\sigma^2}\Vert \eta_j - E\eta_j \Vert^2 \sim \chi^2_{d_j}$, где $d_j = \dim \mathcal{L}_j$.

__Доказательство:__  
Выберем ортонормированный базис в $\R^n$ следуюзим образом:
$$ \underbrace{e_1, e_2, \dots}_{\text{базис в }\mathcal{L}_1} \underbrace{\dots\dots}_{\text{базис в }\mathcal{L}_2} \dots \underbrace{\dots e_n}_{\text{базис в }\mathcal{L}_k}. $$
Обозначим:
* $I_j$ — набор индексов, соответствующий базису в $\mathcal{L}_j$;
* $B = (e_1, \dots, e_n) \in \R^{n \times n}$ — ортогональная матрица;
* $\zeta_i = \langle\xi, e_i\rangle = e^T \xi$ — проекция на $e_i$.

Получаем:
$$ \zeta = \begin{pmatrix} \zeta_1 \\ \vdots \\ \zeta_n \end{pmatrix} = \begin{pmatrix} e_1^T \xi \\ \vdots \\ e_n^T\xi \end{pmatrix} = B^T\xi $$
$$ \xi = \sum_{i=1}^n \langle \xi, e_i \rangle \cdot e_i = \sum_{i=1}^n \zeta_ie_i = (e_1 \dots e_n)\cdot \zeta $$

$\xi = B\zeta$
* $E\zeta = EB^T\xi = B^TE\xi = B^Ta$
* $D\zeta = DB^T\xi = BD\xi B^T = B\sigma^2I_nB^T = \sigma^2 \underbrace{BB^T}_{=I_n} = \sigma^2I_n$

Вывод: $\zeta$ — гауссовский вектор с независимыми компонентами.

$$ \eta_j = \operatorname{proj}_{\mathcal{L}_j} \xi = \sum_{i \in I_j} \langle \xi, e_i \rangle e_i = \sum_{i \in I_j} \zeta_i e_i. $$

Компоненты вектора $\zeta$ в разных $\eta_j$ не пересекаются, следовательно, $\eta_1, \dots, \eta_k$ независимы в совокупности — утв. 1 доказано;

$E\eta_j = \displaystyle\sum_{i \in I_j} \langle E\xi, e_i \rangle e_i = \sum_{i \in I_j} \langle a, e_i \rangle e_i = \operatorname{proj}_{\mathcal{L}_j}a$ — утв. 2 доказано;

$$ \dfrac{1}{\sigma^2}\Vert \eta_j - E\eta_j \Vert^2 = \dfrac{1}{\sigma^2} \bigg\rVert \sum_{i \in I_j} \langle\xi - a, e_i \rangle e_i \bigg\rVert^2 = \sum_{i \in I_j} \underbrace{\left(\dfrac{\zeta_i - E\zeta_i}{\sigma}\right)^2}_{\sim \mathcal{N}(0, 1) \text{ и незав.}} \sim \chi^2_{\dim \mathcal{L}_j}. \quad \square $$

__Доказательство пп. 1-2 из предыдущей теоремы:__

1. $$\R^n = \mathcal{L} \oplus \mathcal{L}^\bot, \text{ где } \mathcal{L} = \left\langle \begin{pmatrix} 1 \\ 1 \\ \vdots \\ 1 \end{pmatrix} \right\rangle .$$

$$\operatorname{proj}_\mathcal{L} X = \argmin_{c \in \R} \left\Vert X - \begin{pmatrix} c \\ c \\ \vdots \\ c \end{pmatrix} \right\Vert^2 = \argmin_{c\in \R} \displaystyle\sum_{i=1}^n (X_i - c)^2 = \begin{pmatrix} \overline{X} \\ \overline{X} \\ \vdots \\ \overline{X} \end{pmatrix}.$$

$$\operatorname{proj}_\mathcal{L^\bot} X = X - \operatorname{proj}_\mathcal{L} X = \begin{pmatrix} X_1 - \overline{X} \\ X_2 - \overline{X} \\ \vdots \\ X_n - \overline{X} \end{pmatrix}. $$

По теореме о разложении гауссовского вектора $X$ и $(X_1 - \overline{X}, \dots, X_n - \overline{X})$ независимы, а $S^2$ зависит только от $(X_1 - \overline{X}, \dots, X_n - \overline{X})$. Вывод: $\overline{X}$ и $S^2$ независимы.

2. Докажем, что $\dfrac{nS^2}{\sigma^2} \sim \chi_{n-1}^2$:
$$ \dfrac{1}{\sigma^2}\Vert \operatorname{proj}_\mathcal{L^\bot} X - E\operatorname{proj}_\mathcal{L^\bot} X \Vert = \dfrac{nS^2}{\sigma^2} \sim \chi_{n-1}^2 $$
по теореме о разложении гауссовского вектора. $\quad \square$