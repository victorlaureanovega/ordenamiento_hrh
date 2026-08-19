# Introducción

Alguien más debió descubrir este algoritmo que llamo «ordenamiento HRH»; me limito a ofrecer el breve estudio que pude realizar con lo poco que sé de algoritmia.

El ordenamiento HRH es bastante parecido al ordenamiento por selección (OS), salvo que, además de buscar el menor elemento de un arreglo, también busca el mayor:

    hrh_sort(A):
    {
        a = 0
        b = n - 1

        Mientras a <= b
        {
            minimo = máximo = a

            Desde i = a hasta i = b
            {
                Si A[i] < A[minimo]:
                    minimo = i

                Si A[i] > A[maximo]:
                    maximo = i
            }

            intercambia(A[a], A[minimo])

            Si maximo == a:
                maximo = minimo

            intercambia(A[b], A[maximo])

            a = a + 1
            b = b - 1
        }
    }

Para determinar el número de comparaciones necesarias para identificar estos elementos debemos notar que, tras cada iteración del bucle principal, el arreglo reduce su tamaño $n$ dos elementos ($a$ avanza y $b$ retrocede).

En el caso de $n$ par, el número de comparaciones $S_1$ puede representarse de la siguiente manera:

$$
S_1=n+(n-2)+(n-4)+...+6+4+2,
$$

donde el k-ésimo elemento es:

$$
a_k=n-2(k-1).
$$

Buscamos encontrar el número de términos sumados, o, lo que es lo mismo, el número de iteraciones completas del bucle cuando $a_k = 2$. Tras el despeje obtenemos que $k=\frac{n}{2}$.

Recordemos que la suma de una progresión aritmética se calcula con la fórmula:

$$
S=\frac{k(a_0+a_k)}{2}.
$$

Sustituyendo:

$$
S_1=\frac{\frac{n}{2}(n+2)}{2}=\frac{n(n+2)}{4}.
$$

En el caso de $n$ impar la progresión será casi la misma, con la diferencia de que el último término será 1:

$$
S_2=n+(n-2)+(n-4)+...+1.
$$

El k-ésimo elemento sigue siendo:

$$
a_k=n-2(k-1).
$$

Nos interesa conocer el número de iteraciones completas cuando $a_k = 1$, así que $k=\frac{n+1}{2}$ y la progresión se convierte en:

$$
S_2=\frac{(n+1)^2}{4}.
$$

Así, el número de comparaciones realizadas por HRH está dado por la siguiente función $h(n)$:

$$
h(n) =
\begin{cases}
      \frac{n(n+2)}{4} & \text{si } n \bmod 2 = 0 \\
      \frac{(n+1)^2}{4} & \text{si } n \bmod 2 \neq 0
\end{cases}
$$

En ambos casos hay un término dominante $f(n)=\frac{n^2}{4}$. Para calcular la complejidad temporal de HRH tomaremos como referencia $g(n)=n^2$ y evaluaremos:

$$
\lim_{n\rightarrow\infty}\frac{f(n)}{g(n)},
$$

que equivale a:

$$
\lim_{n\rightarrow\infty}\frac{n^2}{4n^2}=\frac{1}{4}.
$$

Siendo el resultado un número real finito, concluimos que $h(n) \in \Theta(n^2)$.

HRH reduce el número de comparaciones realizadas por OS, aunque ambos pertenecen al mismo orden exacto. La diferencia práctica entre ambos algoritmos es mínima, lo que probablemente se deba a cómo se realizan las comparaciones en HRH.

Quizás pueda encontrarse en este texto o en el algoritmo el tímido asombro con el que hace unos meses comencé este examen, acaso valioso por su lentitud, acaso valioso por su brevedad.

<br />

V. L. V.

Zapopan, 23 de diciembre de 2024
