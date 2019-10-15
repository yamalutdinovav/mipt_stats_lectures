# Лекция 6 (от 7.10)
### __2.8. Приближенный поиск ОМП__

__Метод Ньютона__:
Пусть $f: \mathbb{R} \rightarrow \mathbb{R}$ — функция. Нужно решить уравнение $f(x) = 0$.

$x_0$ — начальное приближение  
Формула касательной в точке $x_k: y = f(x_k) + f'(x_k)(x-x_k).$ Получим соотношение 
$$x_{k+1} = x_k - \dfrac{f(x_k)}{f'(x_k)}.$$

Пусть $X = (X_1, \dots, X_n)$ — выборка из неизвестного распределения $P \in \{P_\theta \ \vert \ \theta \in \Theta\}, \Theta \subset \mathbb{R}^d$. Пусть $\theta^*$ — ОМП. Хотим приблизить оценку $\theta^*$.

Уравнение правдоподобия: $\dfrac{\partial l_X(\theta)}{\partial \theta} = 0.$ Применим метод Ньютона для функции $l'_X(\theta)$.  
$\widehat{\theta}_0$ — начальное приближение. Шаг метода:
$$ \widehat{\theta}_{k+1} = \widehat{\theta}_k - \underbrace{(l_X''(\widehat{\theta}_k))^{-1}}_{матрица} \cdot \underbrace{l_X'(\widehat{\theta}_k)}_{вектор} .$$

>__Теорема:__ В условиях регулярности $L1-L9$, если $\widehat{\theta}_0$ — а.н.о, то
>
>1. $\widehat{\theta}_1$ — а.н.о с асимт. дисперсией $(i(\theta))^{-1}$.  
>2. $\widehat{\theta}_1$ асимптотически эквивалентна ОМП $\theta^*$, т.е
>$$\sqrt{n}(\widehat{\theta}_1 - \theta^*) \xrightarrow{P_\theta} 0.$$

__Доказательство:__ (для $d=1$, идея)  
_Утв. (б/д)_: $\widehat{\theta}_1 - \theta^* = (\widehat{\theta}_0 - \theta^*)\varepsilon_n(\theta)$, где $\varepsilon_n(\theta)\xrightarrow{P_\theta} 0$.  

(2). $\sqrt{n}(\widehat{\theta}_1 - \theta^*) = \sqrt{n}(\widehat{\theta}_0 - \theta^*)\varepsilon_n(\theta) =\\ {} \\ = \underbrace{\sqrt{n}(\widehat{\theta}_0 - \theta)}_{\xrightarrow{d_\theta} \mathcal{N}(0, \dots)}\underbrace{\varepsilon_n(\theta)}_{\xrightarrow{d_\theta} 0} + \underbrace{\sqrt{n}(\theta - \theta^*)}_{\xrightarrow{d_\theta} \mathcal{N}(0, \dots)}\underbrace{\varepsilon_n(\theta)}_{\xrightarrow{d_\theta} 0}.$  
   По лемме Слуцкого первое слагаемое $\xrightarrow{d_\theta} 0$, второе слагаемое $\xrightarrow{d_\theta} 0$. Применяя еще раз лемму Слуцкого для их суммы, получим $\sqrt{n}(\widehat{\theta}_1 - \theta^*) \xrightarrow{d_\theta (\iff P_\theta, \text{т.к const)}} 0$.

(1). $\sqrt{n}(\widehat{\theta}_1 - \theta) = \underbrace{\sqrt{n}(\widehat{\theta}_1 - \theta^*)}_{\xrightarrow{P_\theta} 0 \text{(из (2))}} - \underbrace{\sqrt{n}(\widehat{\theta}_0 - \theta)}_{\xrightarrow{d_\theta} \mathcal{N}(0, \frac{1}{i(\theta)}) \text{ (ОМП)}}$. По лемме Слуцкого
$$ \sqrt{n}(\widehat{\theta}_1 - \theta) \xrightarrow{d_\theta} \mathcal{N}\left(0, \frac{1}{i(\theta)}\right) \qquad \square.$$

__Замечание__: Утверждение теоремы не изменится, если заменить $l_X''(\theta)$ на $E_\theta l_X''(\theta) = -ni(\theta)$, т.е.
$$  \widehat{\theta}_{k+1} =  \widehat{\theta}_{k} + \dfrac{i(\widehat{\theta}_{k})^{-1}}{n}l'_X(\widehat{\theta}_{k}). $$

Оценка $\widehat{\theta}_{1}$ называется _одношаговой оценкой_. 

__Смысл__:  
Отклонение $\widehat{\theta}_1$ от $\theta^*$ на порядок менььше, чем отклонение $\theta^*$ от $\theta$. Значит отклонение $\widehat{\theta}_1$ от $\theta$ тоже имеет порядок $\sqrt{\frac{1/i(\theta)}{n}}$.

__Пример__ ($\gamma$-котики):  
$\widehat{\mu}$ — а.н.о. с асимпт. дисперсией $\pi^2/4 \approx 2.47$. При этом $i(\theta) = 1/2,$ т.е наименьшая возможная асимпт. дисперсия равна $2$. Запишем одношаговую оценку:

$$ \widehat{\theta}_1 = \widehat{\mu} + \dfrac{\sum\limits_{i=1}^n \frac{X_i - \widehat{\mu}}{1 + (X_i - \widehat{\mu})^2} }{\sum\limits_{i=1}^n  \frac{1 - (X_i - \widehat{\mu})^2}{(1 + (X_i - \widehat{\mu})^2)^2}}. $$

$\widehat{\theta}_1$ — наиболее асимптотически эффективная оценка.

### __2.9. Робастность и симметричные распределения__
Пусть $X = (X_1, \dots, X_n)$ — выборка из $\mathcal{N}(\theta, \sigma^2)$, $\sigma$ известна.  
Оценка $\widehat{\theta} = \overline{X}$ обладает всеми хорошими свойствами (сильная состоятельность, асимптотическая нормальность, ОМП и т. д.). Однако если в данных есть выбросы, то все свойства теряются.  
Для того, чтобы визуализировать выбросы в данных, можно использовать _ящик с усами (box plot)_.

Будем рассматривать только одномерный случай.
>__Определение:__ _Робастная оценка_ — оценка, допускающая отклонение от заданной модели.

>__Определение:__ Пусть оценка имеет вид $\widehat{\theta} = f(X_{(1)}, \dots, X_{(n)})$.  
Пусть $k_n^*$ — наименьшее число $k$, т. ч. выполнено одно из условий:  
>1. Если $x_1, \dots, x_{k+1} \to -\infty$, а $x_{k+2}, \dots, x_n$ фиксированы,то $f(x_1, \dots, x_n) \to -\infty$.
>2. Если $x_{n-k}, \dots, x_n \to +\infty$, а $x_1, \dots, x_{n-k+1}$ фиксированы, то $f(x_1, \dots, x_n) \to +\infty$.  
>
> Тогда число $\tau_{\widehat{\theta}} = \displaystyle\lim_{n\to\infty} \dfrac{k_n^*}{n}$ называется _асимптотической толерантностью оценки $\widehat{\theta}$._

__Смысл:__ $\tau(\theta)$ — наибольшая доля выбросов, которые способна выдержать оценка, не смещаясь на $\pm \infty$.  

__Примеры:__
* $\overline{X}: k_{n}^* = 0, \tau_{\overline{X}} = 0$
* $\widehat{\mu}: k_{n}^* = \lceil n/2 \rceil - 1, \tau_{\widehat{\mu}} = 1/2$.  

Далее будем рассматривать класс распределений $\mathcal{P} = \{P_\theta \vert \theta \in \Theta\}$, т. ч.
* $P_0$ имеет плотность $p_0(x)$ — симметричная, непрерывная, носитель плотности имеет вид $(-c, c),\ 0<c\leqslant +\infty$.
* $\theta$ — параметр сдвига, т. е. $p_\theta(x) = p_0(x-\theta $.
  
Будем искать оценки, которые:
  1. Достаточно эффективные в классе $\mathcal{P}$ (в асимптотическом подходе).
  2. Робастные — допускают отклонение от $\mathcal{P}$.

##### 1. Усеченное среднее
> __Определение:__ Пусть $\alpha \in (0, 1/2),\  k = \lceil \alpha n \rceil.$ Тогда _усеченным средним по выборке $X_1, \dots, X_n$_ называется оценка
> $$ \overline{X}_\alpha = \dfrac{1}{n-2k}(X_{(k-1)} + \dots + X_{(n - k)}).

  * $\alpha = 0$: $\overline{X}_\alpha = \overline{X}$
  * $\alpha = 1/2:$ $\overline{X}_\alpha = \widehat{\mu}.$

Асимптотическая толерантность: $\tau_{\overline{X}_\alpha} = \alpha$.

>__Теорема__ _(б/д)_: Пусть $X = (X_1, \dots, X_n)$ — выборка из  распределения $P \in \mathcal{P}$. Тогда
>$$ \sqrt{n}(\overline{X}_\alpha - \theta) \xrightarrow{d_\theta} \mathcal{N}(0, \sigma^2_\alpha), \text{ где}$$
>$$ \sigma^2_\alpha = \dfrac{2}{(1-2\alpha)^2}\left(\int\limits_0^{\theta} x^2p_0(x)dx + \alpha u^2_{1-\alpha} \right), $$
> $u_{1-\alpha}$ — $(1 - \alpha)$-квантиль распределения $P_0$.

__Пример:__ для $\mathcal{N}(0, 1)$

| $\alpha$ | $0$ | $1/20$ | $1/8$ | $1/4$ | $3/8$ | $1/2$|
|----------|-----|--------|-------|-------|-------|------|
|$\operatorname{ARE}_{\overline{X}_\alpha, \overline{X}}$ | $1$ | $0.99$ | $0.94$ | $0.84$ | $0.74$ | $0.64$ |

При $\alpha = 1/8$ достигается защита от $12.5 \%$ загрязнения выборки, но эффективность теряется на $6 \%$.

__Утв__: Если $D_\theta X_1 < +\infty$, то $\operatorname{ARE}_{\overline{X}_\alpha, \overline{X}} \geqslant (1-2\alpha)^2.$  

$\triangle\quad \overline{X}_\alpha$  — а.н.о $\theta$ с асимпт. дисперсией $\sigma_\alpha^2$.  
Из ЦПТ: $\overline{X}$ — а.н.о $\theta$ с асимпт. дисперсией $D_\theta X_1$. Так как дисперсия не зависит от сдвига, посчитаем дисперсию при $\theta = 0$:
$$ \dfrac{1}{2}D_\theta X_1 = \dfrac{1}{2} \int\limits_{\mathbb{R}} x^2p_0(x)dx = \int\limits_0^{+\infty}x^2p_0(x)dx = \\
= \int\limits_0^{u_{1-\alpha}}x^2p_0(x)dx + \int\limits_{u_{1-\alpha}}^{+\infty}x^2p_0(x)dx \geqslant \\
\geqslant \int\limits_0^{u_{1-\alpha}}x^2p_0(x)dx + u_{1-\alpha}^2\underbrace{\int\limits_{u_{1-\alpha}}^{+\infty}p_0(x)dx}_{=\alpha} = \int\limits_0^{u_{1-\alpha}}x^2p_0(x)dx + \alpha u^2_{1 - \alpha}
= \dfrac{\sigma^2_\alpha (1 - 2\alpha)^2}{2}. $$

Отсюда $\operatorname{ARE}_{\overline{X}_\alpha, \overline{X}} = \dfrac{D_\theta X_1}{\sigma^2_\alpha} \geqslant (1 - 2\alpha)^2 \qquad \square.$

| $\alpha$ | $0$ | $1/20$ | $1/8$ | $1/4$ | $3/8$ | $1/2$|
|----------|-----|--------|-------|-------|-------|------|
|$(1 - 2\alpha)^2$ | $1$ | $0.81$ | $0.56$ | $0.25$ | $0.06$ | $0$ |

При $\alpha = 1/8$ возможна потеря эффективности до $44 \%$.

##### 2. Медиана средних Уолша

> __Определение:__ $Y_{ij} = \dfrac{X_i + X_j}{2}$ — _среднее Уолша_.
>
> $W = \operatorname{med} \{Y_{ij},\ 1 \leqslant i \leqslant j \leqslant n\}$ — _медиана средних Уолша._

>__Теорема:__ Пусть $X = (X_1, \dots, X_n)$ — выборка из  распределения $P \in \mathcal{P}$. Тогда
>$$ \sqrt{n}(W - \theta) \xrightarrow{d_\theta} \mathcal{N}(0, \sigma^2), \text{ где}$$
>$$ \sigma^2 = \dfrac{1}{12\left(\int\limits_\mathbb{R} p_0^2(x)dx\right)^2}. $$

__Пример:__ $\mathcal{N}(0,1): \operatorname{ARE}_{W, \overline{X}} \approx 0.955$ (потеря эффективности на $4.5 \%$).

__Утверждение:__ Для $P_\theta \in \mathcal{P} \operatorname{ARE}_{W, \overline{X}} \geqslant \frac{108}{125} = 0.864$ (в худшем случае теряем $14\%$ эффективности). Равенство достигается при
$$ p_0(x) = \dfrac{3\sqrt{5}}{100}(5 - x^2)I\{|x| < \sqrt{5}\}.$$

__Утверждение:__ $\tau_{W} \approx 0.293$ (доказательство см. в ДЗ).

## Глава 3. Сложные оценки параметров
### __3.1. Доверительные интервалы__

>__Определение:__  Пусть $X = (X_1, \dots, X_n)$ — выборка из неизвестного распределения $P \in \{P_\theta \ \vert \ \theta \in \Theta\}$.
> * Если $\Theta \subset \mathbb{R}$, то пара статистик $(T_1(X), T_2(X))$ называется _доверительным интервалом для $\theta$ уровня доверия $\alpha$,_ если
> $$\forall \theta \in \Theta \quad P_\theta(T_1(X) \leqslant \theta \leqslant T_2(X) ) \geqslant \alpha.$$
> * Если $\Theta \subset \mathbb{R}^d$, то статистика $S(X) \subset \Theta$ называется _доверительной областью для $\theta$ уровня доверия $\alpha$,_ если
> $$\forall \theta \in \Theta \quad P_\theta(\theta \in S(X) ) \geqslant \alpha. $$
> * Если равенство точное, то интервал называтся _точным_.

__Замечание:__  
1. Если $X = (X_1, \dots, X_n)$ — выборка, то утверждение $P_\theta(T_1(X) \leqslant \theta \leqslant T_2(X) ) = \alpha$ имеет смысл ($(T_1(X), T_2(X))$ — доверительный интервал).
2. Если $x = (x_1, \dots, x_n)$ — реализация выборки, то утверждение $P_\theta(T_1(x) \leqslant \theta \leqslant T_2(x) ) = \alpha$ некорректно.

$(T_1(x), T_2(x))$ — _реализация доверительного интервала_.

__Первая магическая константа статистики:__ $\alpha = 0.95 \text{ (она же } 0.05).$