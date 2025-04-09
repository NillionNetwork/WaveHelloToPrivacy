# Accuracy Experiments

We compare Haar and bior(5,3) DWT with quantization, i.e., truncating trailing
bits of the number and evaluating the function at the remaining value.
The precision is $f = 24$, and all LUT outputs have $l = 64$ bits. The input bit
width $n$ depends on the function’s domain. For a real-valued univariate
function $g(x)$ over domain $[a,b]$, we sample $2^n$ equidistant values to
construct quantized, Haar, and Biorthogonal LUTs. We report the Mean and Max
Absolute Errors attained using these compression techniques, focusing on ML
activation functions
(https://paperswithcode.com/methods/category/activation-functions) that are not
piece-wise linear. We exclude ReLU and similar activations as they can be
calculated accurately via splines, focusing on more complex non-linearities.
To set lookup table domains and sizes, we use a threshold
$𝑇 =2^{−18} ≈3.81×10^{−6}$, choosing domains as powers of $2$ so errors
outside fall under this threshold.

For $𝑗$-bit compression in quantization, the quantized LUT is built by
evaluating the function at values after truncating the $𝑗$ trailing bits of the
input. That is, we evaluate the function at $2^𝐽$ equidistant points, where
$𝐽 =𝑛−𝑗$, each point with $𝑗$ trailing bits equal to $0$. On the other hand,
for $𝑗$-bit compression in DWT, we apply the DWT transform $𝑗$ times. We end up
with $2^𝐽$ approximation coefficients, which becomes our LUT. We then normalize
the LUT. In Haar, this normalization consists of multiplication with $2^{−𝑗/2}$.
This value comes from normalizing to $1$ the approximation coefficients of the
one-hot vector after Haar DWT is applied $𝑗$ times.

For GeLU and tanh, we focus on the domain $[−8,8]$. The maximum absolute error
we get outside of this domain for these functions are $5.33×10^{−15}$ and
$2.25×10^{−7}$ respectively. For sigmoid, SiLU, softplus and Mish we use the
domain $[−16,16]$ resulting in errors of $1.13×10^{−7}$, $1.80×10^{−6}$,
$1.13×10^{−7}$, and $1.80×10^{−6}$ respectively. In the case of SELU, we limit
our attention to $[−16,0]$ as it is linear for positive numbers, getting an
error of $1.98×10^{−7}$ for values less than $−16$. For exponential, it is also
enough to consider $[−16,0]$ as $𝑒^{−16} ≈ 1.13 × 10^{−7}$, which is the maximum
absolute error incurred. For reciprocal, we only consider the domain $[1,64]$
because this resembles the range of input that it’s going to take in a softmax
function of up to $64$ values.

We observe that Haar DWT is able to compress a single extra bit more than
quantization with about the same error, while Biorthogonal DWT approximately
halves the bit size of the LUT for less error. This reduction in LUT size leads
to considerable speedup of the lookup table evaluation and the key-size
required.

## Steps

1. Create a virtual Python environment.

```
python -m venv myenv
```

2. Activate the virtual environment.

```
source myenv/bin/activate
```

3. Install requirements.

```
pip install -r requirements.txt
```

4. Generate the data.

```
python accuracy.py
```

5. Inspect the image at `data/lutsize.pdf`.

6. Explore the data for each function such as exponential or gelu.

```
python explore.py <function_name>
```

7. CSV files can be created for inspection.

```
python write_to_csv.py
```
