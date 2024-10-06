# THEORETICAL QUESTIONS - ANSWERS (WILLIAM LIAW)

## Ordinary Least Squares

Before demonstrating that the Ordinary Least Squares (OLS) estimator has the smallest variance among all linear unbiased estimators, we first analyze the OLS estimator:

$$
\begin{align*}
y &= X\beta + \varepsilon \\
y - \varepsilon &= X\beta \\
X^T(y - \varepsilon) &= X^TX\beta \\
(X^TX)^{-1}X^T(y - \varepsilon) &= \beta \\
(X^TX)^{-1}X^Ty - (X^TX)^{-1}X^T\varepsilon &= \beta \\
(X^TX)^{-1}X^Ty &= \beta + (X^TX)^{-1}X^T\varepsilon \\
\beta^* &= \beta + (X^TX)^{-1}X^T\varepsilon \\
\end{align*}
$$

We can observe that the OLS is unbiased $\mathbb{\beta^*}=\beta$ only if $X$ is deterministic and $\mathbb{E}(\varepsilon)=0$. In this case, assuming $\mathbb{V}(\varepsilon)=\sigma^2 I$, we can calculate the variance of the OLS estimator:

$$
\begin{align*}
\mathbb{V}(\beta^*) &= \mathbb{E}((\beta^* - \mathbb{E}(\beta^*))(\beta^* - \mathbb{E}(\beta^*))^T) \\
&= \mathbb{E}((\beta^* - \beta)(\beta^* - \beta)^T) \\
&= \mathbb{E}((\beta + (X^TX)^{-1}X^T\varepsilon - \beta)(\beta + (X^TX)^{-1}X^T\varepsilon - \beta)^T) \\
&= \mathbb{E}(((X^TX)^{-1}X^T\varepsilon)((X^TX)^{-1}X^T\varepsilon)^T) \\
&= \mathbb{E}(((X^TX)^{-1}X^T\varepsilon)(\varepsilon^TX(X^TX)^{-1})) \\
&= (X^TX)^{-1}X^T\mathbb{E}(\varepsilon\varepsilon^T)X(X^TX)^{-1} \\
&= \sigma^2(X^TX)^{-1} \\
\end{align*}
$$

Then, we compute the expected value and variance of the alternative estimator $\tilde{\beta}$.

### Expected value

First, we compute the expected value of $\tilde{\beta}$:

$$
\begin{align*}
\mathbb{E}(\tilde{\beta}) &= \mathbb{E}(Cy) \\
&= C\mathbb{E}(y) \\
&= (H + D)\mathbb{E}(y) \\
&= ((X^TX)^{-1}X^T + D)\mathbb{E}(y) \\
&= ((X^TX)^{-1}X^T + D)\mathbb{E}(X\beta + \varepsilon) \\
&= ((X^TX)^{-1}X^T + D)X\beta \\
&= (I + DX)\beta \\
\end{align*}
$$

Thus, for $\tilde{\beta}$ to be unbiased $(I + DX)\beta=I\beta$, it is necessary that $DX=0$.

### Variance

Consequently, we compute the variance of $\tilde{\beta}$:

$$
\begin{align*}
\mathbb{V}(\tilde{\beta}) &= \mathbb{V}(Cy) \\
&= C\mathbb{V}(y)C^T \\
&= C\mathbb{E}((y - \mathbb{E}(y))(y - \mathbb{E}(y))^T)C^T \\
&= C\mathbb{E}((X\beta + \varepsilon - \mathbb{E}(X\beta + \varepsilon))(X\beta + \varepsilon - \mathbb{E}(X\beta + \varepsilon))^T)C^T \\
&= C\mathbb{E}((\varepsilon - \mathbb{E}(\varepsilon))(\varepsilon - \mathbb{E}(\varepsilon))^T)C^T \\
&= C\mathbb{V}(\varepsilon)C^T \\
&= \sigma^2CC^T \\
&= \sigma^2(H + D)(H + D)^T \\
&= \sigma^2(HH^T + HD^T + DH^T + DD^T) \\
&= \sigma^2(HH^T + (XX^T)^{-1}X^TD^T + DX(XX^T)^{-1} + DD^T) \\
&= \sigma^2(HH^T + DD^T) \\
&= \sigma^2HH^T + \sigma^2 DD^T \\
&= \mathbb{V}(\beta^*) + \sigma^2 DD^T \\
\end{align*}
$$

### Conclusion

From the last expression, it's evident that $\mathbb{V}(\tilde{\beta})$ is always greater than or equal to $\mathbb{V}(\beta^*)$ since $D$ is non-zero, hence $DD^T$ introduces additional variance.

The assumption of OLS that we need to use here is that $X$ is deterministic and $\mathbb{E}(\varepsilon)=0$

## Ridge regression

### Biased estimator

To show that the estimator of ridge regression, denoted as $\beta^*_{\text{ridge}}$, is biased, we need to demonstrate that its expected value, $E(\beta^*_{\text{ridge}})$, does not equal the true parameter vector $\beta$.

Analyzing the ridge estimator $\beta_{\text{ridge}}^* = \arg\min_{\beta} \|y - X\beta\|^2_2 + \lambda \|\beta\|^2_2$ and denoting $f(\beta) = \|y - X\beta\|^2_2 + \lambda \|\beta\|^2_2$, we have:

$$
\begin{align*}
f(\beta) &= \|y - X\beta\|^2_2 + \lambda \|\beta\|^2_2 \\
&= (y - X\beta)^T(y - X\beta) + \lambda \beta^T\beta \\
&= (y^T - \beta^TX^T)(y - X\beta) + \lambda \beta^T\beta \\
&= (y^Ty - y^TX\beta - \beta^TX^Ty + \beta^TX^TX\beta) + \lambda \beta^T\beta \\
\therefore f'(\beta) &= 2 X^TX\beta - 2 X^T y + 2 \lambda \beta \\
\Rightarrow \beta_{\text{ridge}}^* &= (X^TX+\lambda I)^{-1}X^Ty \\
\end{align*}
$$

Now, let's calculate the expected value of the ridge regression estimator:

$$
\begin{align*}
\mathbb{E}(\beta^*_{\text{ridge}}) &= \mathbb{E}((X^TX + \lambda I)^{-1}X^Ty) \\
&= \mathbb{E}((X^TX + \lambda I)^{-1}X^T(X\beta + \varepsilon)) \\
&= \mathbb{E}((X^TX + \lambda I)^{-1}X^TX\beta) \\
&= (X^TX + \lambda I)^{-1}X^TX\beta \\
\end{align*}
$$

Therefore, the expected value of the ridge estimator is generally different than $\beta$ and, consequently, biased. It can be equal to $\beta$ and unbiased, only if $\lambda=0$, in which case the ridge estimator becomes exactly the OLS estimator.

### SVD decomposition

Given the Singular Value Decomposition (SVD) $X = UDV^T$, we can rewrite the expression for $\beta_\text{ridge}^*$:

$$
\begin{align*}
\beta_{\text{ridge}}^* &= (X^TX+\lambda I)^{-1}X^Ty \\
&= ((UDV^T)^TUDV^T+\lambda I)^{-1}(UDV^T)^Ty \\
&= ((VDU^T)UDV^T+\lambda I)^{-1}(VDU^T)y \\
&= (VD^2V^T + \lambda I)^{-1}(VDU^T)y \\
&= V(D^2 + \lambda I)^{-1}V^T(VDU^T)y \\
&= V(D^2 + \lambda I)^{-1}DU^Ty \\
\end{align*}
$$

This solution is particularly useful when the matrix $X$ is ill-conditioned or nearly singular,. In this case, the SVD decomposition provides a numerically stable way to solve the ridge regression problem without directly inverting a potentially singular matrix. Additionally, SVD can be more computationally efficient for large datasets compared to directly computing the inverse of $X^TX+\lambda I$, which is no longer necessary through this method.

### Comparison between OLS variance and Ridge variance

First we calculate the variance of the Ridge estimator:

$$
\begin{align*}
\mathbb{V}(\beta_{\text{ridge}}^*) &= \mathbb{V}((X^TX+\lambda I)^{-1}X^Ty) \\
&= (X^TX+\lambda I)^{-1}X^T\mathbb{V}(y)((X^TX+\lambda I)^{-1}X^T)^T \\
&= (X^TX+\lambda I)^{-1}X^T\mathbb{V}(y)X(X^TX+\lambda I)^{-1} \\
&= (X^TX+\lambda I)^{-1}X^T\mathbb{V}(\varepsilon)X(X^TX+\lambda I)^{-1} \\
&= \sigma^2(X^TX+\lambda I)^{-1}X^TX(X^TX+\lambda I)^{-1} \\
&= \sigma^2((UDV^T)^TUDV^T+\lambda I)^{-1}(UDV^T)^TUDV^T((UDV^T)^TUDV^T+\lambda I)^{-1} \\
&= \sigma^2((VDU^T)UDV^T+\lambda I)^{-1}(VDU^T)UDV^T((VDU^T)UDV^T+\lambda I)^{-1} \\
&= \sigma^2V(D^2+\lambda I)^{-1}D^2(D^2+\lambda I)^{-1}V^T \\
&= \sum\limits_{i=1}^{\text{rank}(X)}\frac{d_i^2\sigma^2}{(d_i^2 + \lambda)^2}v_iv_i^T \\
\end{align*}
$$

We know that the OLS estimator is the Ridge estimator for $\lambda=0$, thus:

$$
\mathbb{V}(\beta_{\text{OLS}}^*) = \sum\limits_{i=1}^{\text{rank}(X)}\frac{\sigma^2}{d_i^2}v_iv_i^T
$$

Hence, it is apparent that for $\lambda \geq 0$, the variance of the Ridge estimator is smaller than or equal to the variance of the OLS estimator, that is $\mathbb{V}(\beta_{\text{ridge}}^*) \leq \mathbb{V}(\beta_{\text{OLS}}^*)$.

### Effect of the regularization parameter

Recalling the expression for the expected value of the Ridge estimator:

$$
\begin{align*}
\mathbb{E}(\beta^*_{\text{ridge}}) &= (X^TX + \lambda I)^{-1}X^TX\beta \\
&= ((UDV^T)^TUDV^T + \lambda I)^{-1}(UDV^T)^TUDV^T\beta \\
&= ((VDU^T)UDV^T + \lambda I)^{-1}(VDU^T)UDV^T\beta \\
&= (VD^2V^T + \lambda I)^{-1}VD^2V^T\beta \\
&= V(D^2 + \lambda I)^{-1}D^2V^T\beta \\
&= \sum\limits_{i=1}^{\text{rank}(X)}\frac{d_i^2}{d_i^2 + \lambda}v_iv_i^T\beta
\end{align*}
$$

One can write the expression for the bias and variance of the ridge estimator:

$$
\begin{align*}
\text{b}(\beta^*_{\text{ridge}}, \beta) &= \mathbb{E}(\beta^*_{\text{ridge}}) -\beta \\
&= \sum\limits_{i=1}^{\text{rank}(X)}\frac{d_i^2}{d_i^2 + \lambda}v_iv_i^T\beta - \beta
\end{align*}
$$

$$
\mathbb{V}(\beta_{\text{ridge}}^*) = \sum\limits_{i=1}^{\text{rank}(X)}\frac{d_i^2\sigma^2}{(d_i^2 + \lambda)^2}v_iv_i^T
$$

Inference suggests that for small $\lambda$ values, the ridge estimator closely resembles the OLS estimator, exhibiting low bias but high variance. Conversely, as $\lambda$ increases, the bias of the ridge estimator amplifies in magnitude while its variance diminishes ($\lambda \rightarrow +\infty \Rightarrow \mathbb{V}(\beta_{\text{ridge}}^*) \rightarrow 0$).

### Derivation of Ridge estimator and OLS estimator expression under $X^T X = I$

As already seen on previous sections:

$$
\beta_{\text{ridge}}^* = (X^TX+\lambda I)^{-1}X^Ty
$$

$$
\beta_{\text{OLS}}^* = (X^TX)^{-1}X^Ty
$$

Assuming $X^TX=I$, these last expressions become:

$$
\begin{align*}
\beta_{\text{ridge}}^* &= (X^TX+\lambda I)^{-1}X^Ty \\
&= (I+\lambda I)^{-1}X^Ty \\
&= ((1+\lambda) I)^{-1}X^Ty \\
\end{align*}
$$

$$
\begin{align*}
\beta_{\text{OLS}}^* &= (X^TX)^{-1}X^Ty \\
&= X^Ty \\
\end{align*}
$$

Therefore:

$$
\beta_{\text{ridge}}^* = \frac{\beta_{\text{OLS}}^*}{1 + \lambda}
$$

## Elastic Net

Analyzing the Elastic Net estimator $\beta_{\text{ElNet}}^* = \arg\min_{\beta} \|y - X\beta\|^2_2 + \lambda_2 \|\beta\|^2_2 + \lambda_1 \|\beta\|_1$ and denoting $f(\beta) = \|y - X\beta\|^2_2 + \lambda_2 \|\beta\|^2_2 + \lambda_1 \|\beta\|_1$, we have:

$$
\begin{align*}
f(\beta) &= \|y - X\beta\|^2_2 + \lambda_2 \|\beta\|^2_2 + \lambda_1 \|\beta\|_1 \\
&= (y - X\beta)^T(y - X\beta) + \lambda_2 \beta^T\beta + \lambda_1 \|\beta\|_1 \\
&= (y^T - \beta^TX^T)(y - X\beta) + \lambda_2 \beta^T\beta + \lambda_1 \|\beta\|_1 \\
&= (y^Ty - y^TX\beta - \beta^TX^Ty + \beta^TX^TX\beta) + \lambda_2 \beta^T\beta + \lambda_1 \|\beta\|_1 \\
\therefore \partial f(\beta) &=
2 X^TX\beta - 2 X^T y + 2 \lambda_2 \beta \pm \lambda_1 \\
\Rightarrow \beta_{\text{ElNet}}^* &= (X^TX+\lambda_2 I)^{-1}(X^Ty \mp \frac{\lambda_1}{2}) \\
\end{align*}
$$

Assuming $X^TX=I$, this last expression becomes:

$$
\begin{align*}
\beta_{\text{ElNet}}^* &= (X^TX+\lambda_2 I)^{-1}X^T(y \mp \frac{\lambda_1}{2}) \\
&= (I+\lambda_2 I)^{-1}X^T(y \mp \frac{\lambda_1}{2}) \\
&= ((1+\lambda_2) I)^{-1}X^T(y \mp \frac{\lambda_1}{2}) \\
\end{align*}
$$

Therefore:

$$
\beta_{\text{ElNet}}^* =  \frac{\beta_{\text{OLS}}^* \mp \frac{\lambda_1}{2}}{1+\lambda_2}
$$

