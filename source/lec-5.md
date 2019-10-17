# Лекция 5 (от 30.09)
### __2.6. Экспоненциальный класс распределений__

>__Определение:__ Семейство распределений $\mathcal{P} = \{P_\theta \vert \theta \in \Theta \}$ принадлежит _экспоненциальному классу_, если плотность $p_\theta(x)$ имеет вид
>$$p_\theta(x) = \dfrac{g(x)}{h(\theta)}e^{a(\theta)^Tu(x)}, $$
>где $g(x) > 0,\ u(x)$ — произвольные борелевские функции,  
$h(\theta) = \int\limits_\mathscr{X}g(x)e^{a(\theta)^Tu(x)}dx$ — нормировочная константа.  
> Если $a(\theta) = \theta$, будем говорить что _параметризация естественная_.

__Пример:__ $\mathcal{P} = \{\mathcal{N}(a, \sigma^2 \vert a \in \R, \sigma > 0\}$. Перейдем к естественным параметрам:
$$p(x) = \dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\dfrac{(x-a)^2}{2\sigma^2}\right) = \dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\dfrac{x^2}{2\sigma^2} + \dfrac{xa}{\sigma^2} - \dfrac{a^2}{2\sigma^2}\right).$$
Введем параметры $\theta = (\theta_1, \theta_2)$: $\theta_1 = -\dfrac{1}{2\sigma^2},\ \theta_2 = \dfrac{a}{\sigma^2}.$
$$ p(x) = \sqrt{-\dfrac{\theta_1}{\pi}}e^{\theta_1x^2 + \theta_2x + \frac{\theta_2^2}{4\theta_1}}. $$ 

$u(x) = \begin{pmatrix}
x^2 \\
x
\end{pmatrix}, a(\theta) = \theta,\ g(x) = 1,\ h(\theta)= \sqrt{-\dfrac{\theta_1}{\pi}}e^{\frac{\theta_2^2}{4\theta_1}}$.  
Найдем достаточные статистики для семейства $\mathcal{P}$:
$$p_\theta(x_1, \dots, x_n) = h^{-n}(\theta)\prod_{i=1}^{n}g(x_i)e^{a({\theta})^T\sum\limits_{i=1}^nu(x_i)}.$$  
По критерию факторизации Неймана-Фишера $S(X) = \sum u(X_i)$ — достаточная статистика.

__Замечание:__ $S(X)$ — статистика фиксированной размерности.

>__Теорема:__ Пусть $\mathcal{P} = \{P_\theta \vert \theta \in \Theta \}$ — семейство распределений т.ч. плотность $p_\theta(x)$ непрерывно дифференцируема по $x$ и носитель не зависит от $\theta$. Пусть также $S(X)$ — достаточная статистика фиксированной размерности $m$. Тогад семейство $\mathcal{P}$ принадлежит экспоненциальному классу.  

 __Следствие:__ Если плотность достаточно хорошая, то только семейства из экспоненциального класса допускают сжатие данных с помощю достаточных статистик.

 __Примеры__:  
 1. $\mathcal{P} = \{\text{Коши со сдвигом}\}$ не лежит в экспоненциальном классе $\implies$ нет достаточных статистик фиксированного размера.
 2. $\mathcal{P} = \{U[0, \theta]\}$ — носитель зависит от $\theta$. Однако достаточная статистика фикс. размера существует: $S(X) = X_{(n)}$.

Далее потребуем некоторые условия:
1. Параметризация естественная
2. $g(x),\ u(x)$ непрерывны
3. Условие равномерной сходимости интеграла по параметру:
$$ \forall s\  \forall j \leqslant k\  \exists \varphi(x): \forall \theta \in \Theta \ |g(x)u_s^j(x)e^{\theta u(x)}| \leqslant \varphi(x), $$
и при этом $\int\limits_{\mathscr{X}}\varphi(x)dx$ сходится.

__Следствия:__  
1. $h(\theta)$ непрерывно дифференцируема $k$ раз
2. $p_\theta(x)$ непрерывно дифференцируема $k$ раз по $\theta$
3. Можно менять местами $\frac{\partial}{\partial \theta}$ и $\int$

>__Утверждение 1:__
>1. $$E_\theta u(X_1) = \nabla \ln h(\theta) = \left(\frac{\partial}{\partial \theta} \ln h(\theta)\right)_j$$
>2. $$D_\theta u(X_1) = \nabla^2 \ln h(\theta) = \left(\frac{\partial^2}{\partial \theta^2} \ln h(\theta)\right)_{jk}$$

$\triangle$ (1): 
$$\frac{\partial h(\theta)}{\partial \theta_j} = \frac{\partial}{\partial \theta}\int\limits_\mathscr{X} g(x)e^{\theta^Tu(x)}dx = \{\text{следствие 3}\} = \int\limits_\mathscr{X} u_j(x)g(x)e^{\theta^Tu(x)}dx = h(\theta)\int\limits_\mathscr{X}\dfrac{u_j(x)}{h(\theta)})g(x)e^{\theta^Tu(x)}dx = h(\theta)E_\theta u_j(X_1).$$
$$ E_\theta u_j(X_1) = \dfrac{\partial h(\theta) / \partial \theta_j}{h(\theta)} = \dfrac{\partial \ln h(\theta)}{\partial \theta} \qquad \square. $$

__Утверждение__: Если $\Theta$ — выпуклое множество, то ОМП существует и единственна.  

$\triangle$ $\ \nabla \nabla \ln h(\theta) = D_\theta u(X_1) \geqslant 0 \implies \ln h(\theta)$ выпукла. 

$l_X(\theta)= \underbrace{\sum \ln g(X_i)}_{\text{не зависит от }\theta} \underbrace{-n\overbrace{\ln h(\theta)}^{выпукла}}_{вогнута} + \underbrace{\theta\sum u(X_i)}_{\text{линейна по }\theta} \implies l_X(\theta)$ вогнута.

Значит, максимум существует и единственный$\quad \square$.

__Утверждение__: Если $\Theta$ — выпуклое открытое множество, то выполнены условия L5-L9.

$\triangle \quad$ L5-L7 выполнены из следствий 1-3  

L8: $\frac{\partial \ln p_\theta(x)}{\partial \theta} = \frac{\partial}{\partial \theta}(\ln g(x) - n\ln h(\theta) + \theta u(x)) = \frac{\partial h(\theta)}{h(\theta)} + u(x)$  

$i(\theta) = E_\theta(\frac{\partial \ln p_\theta(X_1)}{\partial \theta})^2$ по утверждению 1 существует и конечна

L9 следует из того, что $\frac{\partial^2 \ln p_\theta(X_1)}{\partial \theta^2}$ не зависит от $\theta \quad \square$.

### __2.7. Сравнение оценок__
Ранее было:  
$X_1, \dots, X_n \sim Exp(\theta)$.  

$\widehat{\theta}_1 = 1/\overline{X}, \ \widehat{\theta}_2 = -\ln \overline{I\{X > 1\}}$ — (сильно) состоятельная, а. н. оценка $\theta$. Хотим построить оценку для $\tau(\theta) \in \R^d$.

>__Определение:__ Функция $L: \R^d \times \R^d \rightarrow \R_+$, которая характеризует степень отклонения оценки от $\tau(\theta)$, называется _функцией потерь (loss function)_.

__Примеры:__
1. $L(x, y) = (x - y)^2$ — квадратичная функция потерь
2. $L(x, y) = |x - y|$ — абсолютная функция потерь
3. $L(x, y) = \log(1 + |x - y|)$  
многомерный случай:
4. $L(x, y) = (x - y)^TA(x - y)$, $A$ — симметричная, полож. определенная матрица  
если $A = I_d: L(x, y) = \sum\limits_{j = 1}^d (x_j - y_j)^2$.

Пусть $\widehat{\theta}$ — оценка $\tau(\theta)$, $\theta$ — истинное значение параметра. Тогда $L(\widehat{\theta}, \theta)$ — штраф при оценивании $\tau(\theta)$ оценкой $\widehat\theta$.  
Проблема: штраф случаен

>__Определение:__ Функция риска
>$$R_{\widehat\theta, \tau}(\theta) = E_\theta L(\widehat\theta, \tau(\theta)).

__Примеры:__
* $\operatorname{MSE}_{\widehat{\theta}, \tau}(\theta) = E_\theta(\widehat{\theta} - \tau(\theta))^2$ — _среднеквадратичная ошибка_
* $\operatorname{MAE}_{\widehat{\theta}, \tau}(\theta) = E_\theta|\widehat{\theta} - \tau(\theta)|$ — _средняя абсолютная ошибка_

__Замечание:__ если $\tau(\theta) = \theta$, то индекс $\tau$ опускаем.

__Задача:__ $X_1, \dots, X_n$ — выборка. $\widehat{\theta}_1 = X_1, \ \widehat{\theta}_2 = \overline{X}$ — оценки $\tau(\theta) = E_\theta(X_1)$. Посчитать MSE.  

$\triangle \quad \operatorname{MSE}_{\widehat{\theta}_1, \tau}(\theta) = E_\theta(X_1 - E_\theta X_1)^2 = D_\theta X_1$  
$\qquad \operatorname{MSE}_{\widehat{\theta}_2, \tau}(\theta) = E_\theta(\overline{X} - E_\theta \overline{X})^2 = D_\theta \overline{X} = \frac{1}{n}D_\theta X_1.$  

_Вывод:_ усреднение уменьшает среднеквадратичный риск в $n$ раз. $\quad \square$

#### Подходы к сравнению оценок:

#### 1. Равномерный
* $\widehat\theta_1$ _не хуже_ $\widehat\theta_2$, если $\forall \theta R_{\widehat{\theta}_1, \tau (\theta)}\leqslant R_{\widehat{\theta}_2, \tau (\theta)}$.
* $\widehat\theta_1$ _лучше_ $\widehat\theta_2$, если, кроме того, $\exists \theta: R_{\widehat{\theta}_1, \tau (\theta)} < R_{\widehat{\theta}_2, \tau (\theta)}$.
* Пусть $\mathscr{K}$ — множество оценок. $\widehat{\theta}$ — _наилучшая в $\mathscr{K}$_, если она лучше всех оценок из $\mathscr{K}$.
* Если $L(x, y) = (x - y)^2$, то подход называется _среднеквадратичным_.

__Утверждение:__ Наилучшей оценки может не существовать.  
$\triangle \quad \mathscr{K} = \{\widehat{\theta}_1 \equiv 1, \widehat{\theta}_2 \equiv 2\}$  
$\qquad \operatorname{MSE}_{\widehat{\theta}_1}(\theta) = E_\theta(\theta - 1)^2 = (\theta - 1)^2$  
$\qquad \operatorname{MSE}_{\widehat{\theta}_2}(\theta) = E_\theta(\theta - 2)^2 = (\theta - 2)^2$  
Если $\theta < 1.5$, то $\operatorname{MSE}_{\widehat{\theta}_1}(\theta) < \operatorname{MSE}_{\widehat{\theta}_2}(\theta)$; если $\theta > 1.5$, то $\operatorname{MSE}_{\widehat{\theta}_2}(\theta) < \operatorname{MSE}_{\widehat{\theta}_1}(\theta)\quad \square$.

>__Утверждение:__ Справедливо _bias-variance разложение:_
>
>$$ \underbrace{\operatorname{MSE}_{\widehat{\theta}, \tau}(\theta)}_{error} = \underbrace{D_\theta \widehat{\theta}}_{variance} + \underbrace{(E_\theta \widehat{\theta} - \theta)^2}_{bias^2}.$$

$\triangle \quad \operatorname{MSE}_{\widehat{\theta}, \tau}(\theta)= E_\theta(\widehat{\theta} - \tau(\theta))^2 = E_\theta((\widehat{\theta} - E_\theta\widehat{\theta}) + (E_\theta\widehat{\theta} - \tau(\theta))^2 = E_\theta(\widehat{\theta} - E_\theta(\widehat{\theta}))^2 + 2E_\theta(\widehat{\theta} - E_\theta\widehat{\theta})(E_\theta\widehat{\theta} - \tau(\theta)) + (E_\theta(\widehat{\theta}) - \tau(\theta))^2$  
Второе слагаемое равно нулю, следовательно, получаем требуемое. $\quad \square$

__Следствие:__ Среди все несмещенных оценок наилучшей будет та, у которой меньше дисперсия.

#### 2. Байесовский
Пусть $Q$ — некоторое распределение на $\Theta$. Тогда $\widehat{\theta}_1$ не хуже $\widehat{\theta}_2$, если  $E_QR_{\widehat\theta_1}(\theta) \leqslant E_QR_{\widehat\theta_2}(\theta)$.

#### 3. Минимаксный
$\widehat{\theta}_1$ не хуже $\widehat{\theta}_2$, если $\displaystyle\sup_{\theta \in \Theta}R_{\widehat\theta_1}(\theta) \leqslant \displaystyle\sup_{\theta \in \Theta}R_{\widehat\theta_2}(\theta)$.

#### 4. Асимптотический (для а.н.о)
Пусть $\widehat{\theta}_1, \widehat{\theta}_2$ — а.н.о. $\tau(\theta)$ с асимпт. дисперсией $\sigma_1^2$ и $\sigma^2_2$. Тогда 
* $\widehat{\theta}_1$ не хуже  $\widehat{\theta}_2$, если $\sigma_1(\theta) \leqslant \sigma_2(\theta)\ \forall \theta \in \Theta$.
* $\widehat{\theta}_1$ лучше  $\widehat{\theta}_2$, если, кроме того $\exists \theta \in \Theta: \ \sigma_1(\theta) < \sigma_2(\theta)$.
* _Относительная асимптотическая эффективность_: $\operatorname{ARE}_{\widehat{\theta}_1, \widehat{\theta}_2}^{\tau}(\theta) = \dfrac{\sigma_2^2}{\sigma_1^2}$ показывает, насколько $\widehat{\theta}_1$ лучше  $\widehat{\theta}_2$.

$\widehat{\theta}_1$ не хуже  $\widehat{\theta}_2$, если $\operatorname{ARE}_{\widehat{\theta}_1, \widehat{\theta}_2}^{\tau}(\theta) \geqslant 1 \forall \theta \in \Theta$.

>__Определение:__ Оценка $\widehat{\theta}$ называется _асимптотически эффективной оценкой $\tau(\theta)$_, если она имеет наименьшую асимптотическую дисперсию среди всех а.н.о. $\tau(\theta)$ с непрерывной а. д.

__Утверждение:__  Если выполнены условия L1-L9, то ОМП асимптотически эффективна.

__Пример__: $X_1, \dots, X_n \sim \mathcal{N}(\theta, 1)$.
* ОМП: $\widehat{\theta}_1 = \overline{X}$ — а.н.о $\theta$ c а.д. $\sigma_1^2 = 1$.
* Теор. о выборочной медиане: $\widehat\theta_2 = \widehat{\mu}$ — а.н.о $\theta$ с а.д. $\sigma_2^2 = \frac{2\pi}{4} = \frac{\pi}{2}$.

$\operatorname{ARE}_{\overline{X}, \widehat{\mu}}(\theta) = \frac{\sigma_2^2(\theta)}{\sigma_1^2(\theta)} = \frac{\pi}{2} \approx 1.57$.