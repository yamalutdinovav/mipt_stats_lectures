# Лекция 3

>__Теорема (дельта-метод):__ Пусть $\hat{\theta}_n$ — асимптотически нормальная оценка $\theta \in \Theta \sub \mathbb{R}^d$ с асимптотической матрицей ковариаций $\Sigma(\theta)$ и $\tau:\mathbb{R}^d \rightarrow \mathbb{R}^k$ — непрерывно дифференцируемая функция. Тогда $\tau(\hat{\theta}_n)$ — асимптотически нормальная оценка $\tau(\theta)$ с асимптотической матрицей ковариаций $D(\theta)\Sigma(\theta)D^T(\theta)$, где $D(\theta) = \dfrac{\partial \tau(\theta)}{\partial \theta}$.

__Доказательство:__ Применим теорему о производной:
$$a=\theta, \: h(x) = \tau(x), \: \xi_n=\sqrt{n}(\hat{\theta}_n - \theta), \: \xi \sim \mathcal{N}(0, \Sigma(\theta)),\: b_n=\dfrac{1}{\sqrt{n}}$$
$$\dfrac{h(a+\xi_nb_n) - h(a)}{b_n} = \dfrac{\tau\left(\theta + \dfrac{1}{\sqrt{n}}\sqrt{n}(\hat{\theta}-\theta)\right) - \tau(\theta)}{1/\sqrt{n}}=$$
$$=\sqrt{n}(\tau(\hat{\theta}) - \tau(\theta)) \xrightarrow{d} \underbrace{\dfrac{\partial h}{\partial x}\Biggr\rvert_\theta}_{D(\theta)} \xi \sim \mathcal{N}(0, D(\theta)\Sigma(\theta)D^T(\theta)).$$
$\square$

__Пример:__ $X_1,\dots X_n \sim Exp(\theta)$, $\theta > 0$. ЦПТ:
$$\sqrt{n}\left(\overline{X} - \dfrac{1}{\theta}\right) \xrightarrow{d_\theta} \mathcal{N}(0, 1/\theta^2) \Rightarrow \overline{X} \text{— а.н.о. } \frac{1}{\theta} \text{ с асимптотической дисперсией }1/\theta^2.$$
Примерим дельта-метод с функцией $\tau(x) = 1/x$: $\tau(\overline{X}) = \dfrac{1}{\overline{X}}$ — а.н.о. $\tau\left(\dfrac{1}{\theta}\right)$. с асимптотической дисперсией $\dfrac{1}{\theta^2}\cdot \left(\dfrac{\partial \theta}{\partial x}\Biggr\rvert_{1/\theta}\right)^2 = \dfrac{1}{\theta^2}\left(-\dfrac{1}{x^2}\right)^2 = \theta^2$.

__Доказательство теоремы о наследовании сходимостей:__
1) $\xi_n \xrightarrow{P} \xi$ и $h : \mathbb{R}^d \rightarrow \mathbb{R}^k$ непрерывна на $B$ таком, что $P(\xi \in B) = 1$. 
 $$h(\xi_n) \xrightarrow{P} h(\xi) \Leftrightarrow \forall \varepsilon > 0 \underbrace{P(\Vert h(\xi_n) - h(\xi)\Vert) > \varepsilon}_{\forall \delta > 0 \exist N : \forall n > N P(\Vert h(\xi_n)-h(\xi)\Vert) > \varepsilon < \delta} \rightarrow 0.$$
 $$h(\xi_n) \xrightarrow{P} \xi \Rightarrow \exist \varepsilon, \delta, \{\xi_n\}_{k=1}^\infty : P(\Vert h(\xi_n) - h(\xi) \Vert > \varepsilon) > \delta.$$ 
 Заметим, что $\xi_n \rightarrow \xi \Rightarrow$ существует последовательность $\{\xi_{n_{k_s}}\}_{s=1}^\infty$ такая, что $\xi_{n_{k_s}} \xrightarrow{п. н.} \xi$, $s \rightarrow \infty$.

2) $\xi_n\xrightarrow{п.н.} \xi$, $h:\mathbb{R}^d \rightarrow \mathbb{R}^k$ непрерывна на множестве $B:P(\xi \in B) = 1$. $\xi_n \xrightarrow{п. н.} \xi \Leftrightarrow P(\displaystyle{\lim_{n \to \infty} \xi_n = \xi}) = 1$. Хотим доказать, что $P(\displaystyle{\lim_{n \to \infty} h(\xi_n) =h(\xi)) = 1}$. $P(\displaystyle{\lim_{n \to \infty} h(\xi_n) =h(\xi)) = 1} \geqslant P(\displaystyle{\lim_{n \to \infty}\xi_n = \xi, \xi \in B) = 1},$ так как вероятность этого события равна 1.
3) $\xi_n \xrightarrow{d} \xi$ и $h$ непрерывна. Возьмем $f : \mathbb{R}^k \rightarrow \mathbb{R}$ — непрерывная ограниченная. Тогда $f(h(x))$ непрерывная ограниченная на $\mathbb{R}^d$, и, поскольку $\xi_n \xrightarrow{d} \xi$, то $E(h(\xi_n)) \rightarrow Ef(h(\xi)) \Rightarrow h(\xi_n) \xrightarrow{d} h(\xi)$ по определению. 

$\square$


  __Доказательство леммы Слуцкого для суммы:__ $\xi_n \xrightarrow{d} \xi$, $\eta_n \xrightarrow{d} c \Rightarrow \xi_n + \eta_n \xrightarrow{d} \xi + c$.

$\xi_n \xrightarrow{d} \xi \Leftrightarrow F_{\xi_n}(x) \rightarrow F_\xi(x)$ в точках непрерывности $F_\xi$. $F_{\xi+c}(x) = F_\xi(x-c)$. $\xi_n \rightarrow \xi \Rightarrow \xi_n + c \rightarrow \xi + c$, так как есть сходимость в точках непрерывности $F_{\xi + c}(x)$.
$$F_{\xi_n + \eta_n}(t) = P(\xi_n + \eta_n \leqslant t) = P(\xi_n + \eta_n \leqslant t, \:\eta_n < c + \varepsilon) + P(\xi_n + \eta_n \leqslant t, \:\eta_n \geqslant c - \varepsilon) \fbox{$\leqslant$}$$
1. $$\{\xi_n + \eta_n \leqslant t, \; \eta_n < c - \varepsilon\} \sub \{\eta_n < c - \varepsilon\} \sub \{|\eta_n - c| > \varepsilon\}.$$
2. $$\{\xi_n + \eta_n \leqslant t, \; \eta_n \geqslant c - \varepsilon\} \sub \{\xi_n + c - \varepsilon \leqslant t, \; \eta_n \geqslant c - \varepsilon\} \sub \{\xi_n + c \leqslant t + \varepsilon\}.$$

$$\fbox{$\leqslant$} P(|\eta_n-c| > \varepsilon) + P(\xi_n + c \leqslant t + \varepsilon).$$
$$\lim_{n\to \infty} \sup F_{\xi_n + \eta_n}(t) \leqslant \underbrace{\lim_{n\to \infty} P(|\eta_n - c| > \varepsilon)}_{=0\text{ т.к. }\eta_n \xrightarrow{d} c \Rightarrow\eta_n \xrightarrow{P} c} + \underbrace{\lim_{n\to\infty}F_{\xi_n + c}(t + \varepsilon)}_{=F_{\xi + c}(t+\varepsilon)\text{, т.к. }\xi_n+c\xrightarrow{d}\xi+c\text{ и } t + c\text{ — т.непр.}}$$
То есть $\displaystyle{\lim_{n\to\infty}\sup F_{\xi_n + \eta_n}(t) \leqslant F_{\xi+c}(t+\varepsilon)}$. Аналогично $\displaystyle{\lim_{n\to\infty}\inf F_{\xi_n+\eta_n}(t) \geqslant F_{\xi + c}(t - \varepsilon)}$, следовательно $F_{\xi + c}(t - \varepsilon) \Rightarrow F_{\xi+c}(t-\varepsilon) \leqslant \displaystyle{\lim_{n\to\infty}}\inf F_{\xi_n + \eta_n}(t) \leqslant \displaystyle{\lim_{n\to\infty}\sup F_{\xi_n+\eta_n}(t) \leqslant F_{\xi+c}(t+\varepsilon)}$. В силу произвольности $\varepsilon > 0$ и непрерывности $F_{\xi+c}(t)$, получаем, что существует $\displaystyle{\lim_{n\to\infty}}F_{\xi_n+\eta_n}(t) = F_{\xi+c}(t) \Rightarrow \xi_n + \eta_n \xrightarrow{d} \xi + c$. 

$\square$

## 2.4. Методы нахождения оценкок

### (1) Метод моментов
__Идея:__ приравняем друг к другу теоретические и выборочные моменты.

Пусть $X = (X_1, \ldots, X_n)$ — выборка из неизвестного распределения $P \in \{P_\theta| \theta \in \Theta\}$, $\Theta \sub \mathbb{R}^d$. Составим систему:
$$\begin{cases}
    E_\theta X_1 = \overline{X}\\
    E_\theta X_1^2 = \overline{X^2}\\
    \dots\\
    E_\theta X_1^d = \overline{X^d}
\end{cases}$$
Решение этой системы называется оценкой $\theta$ по методу моментов.
#### Обобщенный метод моментов
Пусть $g_1(x),\ldots, g_d(x)$ — борелевские функции, такие, что $|E_\theta g_j(x_j)| < +\infty$. Составим систему:
$$\begin{cases}
    E_\theta g_1(X_1) = \overline{g_1(X)}\\
    E_\theta g_2(X_1) = \overline{g_2(X)}\\
    \dots\\
    E_\theta g_d(X_1) = \overline{g_d(X)}
\end{cases}$$
__Пример:__ $X_1, \ldots, X_n \sim Exp(\theta)$. Найти оценку стандартным методом моментов и обобщенным с функцией $g(x) = I\{x > 1\}.$

__Решение:__ 
1. Стандартный метод моментов дает уравнение $E_\theta X_1 = \overline{X} \Rightarrow \hat{\theta}_1 = \dfrac{1}{\overline{X}}.$  Ранее мы получали, что $\hat{\theta}_1$ — асимптотически нормальная оценка $\theta$ с асимптотической дисперсией $\theta^2 = \sigma^2(\theta)$.
2. Получаем систему из одного уравнения: $E_\theta I(X_1 > 1) = \overline{I(X > 1)}$. $E_\theta I\{X_1 > 1\} = \displaystyle{\int_1^{+\infty}}\theta e^{-\theta x}dx = e^{-\theta}$, $\overline{I\{X>1\}} = \dfrac{1}{n}\displaystyle{\sum_{i=1}^n I\{X_i > 1\}}$. Получаем $\hat{\theta}_2 = \ln \overline{I\{X > 1\}}$. ЦПТ: $\overline{I\{X > 1\}}$ — асимптотически нормальная оценка $e^{-\theta}$ с асимптотической дисперсией $D_\theta I\{X_1 > 1\} = e^{-\theta} - e^{-2\theta}$. Применим дельта-метод с функцией $\tau(x) = -\ln x$. Отсюда $\hat{\theta}_2$ — асимптотически нормальная оценка $\theta$ с асимптотической дисперсией $(e^{-\theta} - e^{-2\theta})\cdot((-\ln x)')^2\Biggr\rvert_{e^{-\theta}} = (e^{-\theta}-e^{-2\theta})\cdot\dfrac{1}{x^2}\Biggr\rvert_{e^{-\theta}} = e^{\theta} - 1 = \sigma_2^2(\theta)$.

__Вывод:__ нужен метод сравнения оценок. Видимо, $\hat{\theta}_1$ лучше $\hat{\theta}_2$, так как $\sigma_1^2(\theta) < \sigma_2^2(\theta)$.

Распишем оценку по методу моментов: пусть $g_1(x), \ldots, g_d(x)$ — борелевские функции такие, что $|E_\theta g_i(x_i)| < +\infty$.
$$m(\theta) = \begin{pmatrix}E_\theta g_1(X_1)\\ \ldots \\ E_\theta g_d(x_1)\end{pmatrix} = \begin{pmatrix}\overline{g_1(X)}\\ \ldots \\ \overline{g_d(x)}\end{pmatrix} = \overline{g(X)} \Rightarrow\hat{\theta} = m^{-1}(g(\overline{X})).$$

> __Утверждение:__
>  1. Если $m^{-1}$ непрерывна, то $\hat{\theta}$ — сильно состоятельная оценка $\theta$.
>  2. Если $m^{-1}$ непрерывно дифференцируема и $E_\theta g_i^2(X_i) < +\infty$, то $\hat{\theta}$ — асимптотически нормальная оценка $\theta$.

__Доказательство:__ 
1. В силу выбора $g_i:|E_\theta g_i(X_i)| < +\infty$ по УЗБЧ: $\overline{g(X)} \xrightarrow{P_\theta-п.н.} m(\theta) = E_\theta g(X_1)$. Поскольку $m^{-1}$ непрерывна, то по теореме о наследовании сходимостей $\hat{\theta} = m^{-1}(\overline{g(X)})$ — сильно состоятельная оценка $m^{-1}(m(\theta))=\theta$.
2. ЦПТ: $\sqrt{n}(\overline{g(X)} - m(\theta) \xrightarrow{d_\theta} \mathcal{N}(0, \Sigma(\theta))\Rightarrow \overline{g(X)}$ — асимптотически нормальная оценка $m(\theta)$. Применяем дельта-метод с функцией $m^{-1}$: $\hat{\theta}$ — асимптотически нормальная оценка $\theta$. $\square$

### (2) Метод максимального правдоподобия
Пусть $X=(X_1, \ldots X_n)$ — выборка из неизвестного распределения $P \in \{P_\theta|\theta \in \Theta\}$, где
1. Либо все $P_\theta$ абсолютно непрерывные и $p_\theta(x)$ — плотность $P_\theta$.
2. Либо все $P_\theta$ дискретные и $p_\theta(x) = P_\theta(X_1 = x)$ — дискретная плотность.
   
> __Определение:__ $L_X(\theta) = p_\theta(X) = \displaystyle{\prod_{i = 1}^n}p_\theta(X_i)$ — функция правдоподобия (как функция от $\theta$).

> __Определение:__ $l_X(\theta) = L_X(\theta)$ — логарифмическая функция правдоподобия.

__Замечание:__ При фиксированном $\theta$ функция правдоподобия равна плотности выборки, в которую в качестве аргумента подставлена сама выборка.

__Смысл:__ "вероятность" выборки в зависимости от значения параметра. Степень доверия к конкретному значению параметра. Интересует только относительное значение.

__Пример:__ пусть $x_1$ — наблюдение.

*Рисунок*

Видимо $\theta_2$ более правдоподобно, чем $\theta_1$ и $\theta_3$.

> __Определение:__ $\hat{\theta} = \argmax_{\theta \in \Theta} L_X(\theta)$ называется оценкой максимального правдоподобия.

> __Утверждение:__ ОМП не зависит от параметризации. Пусть $\hat{\theta}$ — ОМП для $\theta$. $\tau : \Theta \rightarrow \Psi$ — биекция. Тогда $\tau(\hat{\theta})$ — ОМП для $\tau(\theta)$.

> __Утверждение:__ Пусть $\forall n,\;\forall x_1, \ldots,x_n$ уравнение правдоподобия $\displaystyle{\sum_{i=1}^n}\dfrac{\partial}{\partial \theta}\ln p_\theta(x_i) = 0$ имеет только одно решение. Тогда
> 
> 1. $[L1-L5]\Rightarrow$ ОМП состоятельна;
> 2. $[L1-L9]\Rightarrow$ ОМП является асимптотически нормальной оценкой $\theta$ с асимптотической матрицей ковариаций $i(\theta)^{-1}$, где $i(\theta)_{jk} = E_\theta \dfrac{\partial l_{X_1}(\theta)}{\partial \theta_j}\dfrac{\partial l_{X_1}(\theta)}{\partial \theta_k}$.
> 3. $[L1-L9]\Rightarrow$ решение уравнения и есть ОМП.

__Задача:__ $X_1,\ldots,X_n \sim Exp(\theta)$. Найти ОМП для $\theta$ и $1/\theta$.

__Решение:__ $p_\theta(x) = \theta e^{-\theta x}\cdot I\{x>0\}$. Отсюда 
$$L_X(\theta) = \displaystyle{\prod_{i=1}^n}\theta e^{-\theta X_i}\cdot I\{X_i > 0\} = \theta^n e^{-\theta\sum X_i}\cdot I\{\forall i \;X_i > 0\}.$$
Прологарифмируем:
$$l_X(\theta) = n\ln \theta - \theta\sum_{i=1}^n X_i.$$
$$\dfrac{\partial l_X(\theta)}{\partial \theta} = \dfrac{n}{\theta}-\sum_{i = 1}^n X_i = 0 \Rightarrow\hat{\theta} = \dfrac{1}{\overline{X}}.$$
По утверждению о независимости от способа параметризации $\overline{X}$ — ОМП для $1/\theta$, $i(\theta)=E_\theta\left(\dfrac{\partial l_{X_1}(\theta)}{\partial}\right)^2 = E_\theta\left(\dfrac{1}{\theta}-X_1\right)^2 = D_\theta X_1 = \dfrac{1}{\theta^2} \Rightarrow \hat{\theta} = \dfrac{1}{\overline{X}}$ — асимптотически нормальная оценка $\theta$ с асимптотической дисперсией $i(\theta)^{-1} = \theta^2$.