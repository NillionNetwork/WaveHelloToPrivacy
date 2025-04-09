# Wave Hello to Privacy: Efficient Mixed-mode MPC from Wavelet Transforms

by José Reis, Mehmet Ugurbil, Sameer Wagh, Ryan Henry and Miguel de Vega

https://eprint.iacr.org/2025/013.pdf

## Abstract

This paper introduces new protocols for secure multiparty computation (MPC)
leveraging Discrete Wavelet Transforms (DWTs) for computing nonlinear functions
over large domains. By employing DWTs, the protocols significantly reduce the
overhead typically associated with Lookup Table-style (LUT) evaluations in MPC.
We state and prove foundational results for DWT-compressed LUTs in MPC, present
protocols for 9 of the most common activation functions used in ML, and
experimentally evaluate the performance of our protocols for large domain sizes
in the LAN and WAN settings. Our protocols are extremely fast – for instance,
when considering 64-bit inputs, computing 1000 parallel instances of the sigmoid
function, with an error less than $2^{−24}$ takes only a few hundred
milliseconds incurs just 29 KiB of online communication (40 bytes per
evaluation).

## Keywords

Privacy-enhancing technologies, secure multiparty computation, lookup tables,
discrete wavelet transforms

## Accuracy Experiments

This module is to run accuracy experiments measuring the error obtained after
compressing the lookup table using discrete wavelet transforms.

1. Enter accuracy directory.

```
cd accuracy
```

2. Create a virtual Python environment.

```
python3 -m venv myenv
```

3. Activate the virtual environment.

```
source myenv/bin/activate
```

4. Install requirements.

```
pip install -r requirements.txt
```

5. Generate the data.

```
python accuracy.py
```

6. Inspect the image at `data/lutsize.pdf`.

7. Explore the data for each function such as exponential or gelu.

```
python explore.py <function_name>
```

8. CSV files can be created for inspection.

```
python write_to_csv.py
```

## Execution Time Experiments

This module is for running time experiments.

1. Enter experiments directory.

```
cd experiments
```

2. Run the experiments.

```
./run_all.sh
```