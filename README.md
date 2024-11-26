# MolGPT
In this work, we train small custom GPT on Moses and Guacamol dataset with next token prediction task. The model is then used for unconditional and conditional molecular generation. We compare our model with previous approaches on the Moses and Guacamol datasets. Saliency maps are obtained for interpretability using Ecco library.

- The processed Guacamol and MOSES datasets in csv format can be downloaded from this link:

https://drive.google.com/drive/folders/1LrtGru7Srj_62WMR4Zcfs7xJ3GZr9N4E?usp=sharing

- Original Guacamol dataset can be found here:

https://github.com/BenevolentAI/guacamol

- Original Moses dataset can be found here:

https://github.com/molecularsets/moses

- All trained weights can be found here:

https://www.kaggle.com/virajbagal/ligflow-final-weights

# Requirements

You need to install moses by doing:

```
git clone https://github.com/molecularsets/moses.git
cd moses
python setup.py install
```

As well as guacamole

```
pip install guacamol
```

The code only works with Panda's versions 1.5.3 and below so you may need to downgrade it.

To train the model, make sure you have the datasets' csv file in the same directory as the code files.

# Training
The commands below work for training (first chmod +x the files), although with the checkpoints I got from them I could not get it to generate unconditional molecules.


```
./train_moses.sh
```

```
./train_guacamol.sh
```

# Generation
For generation to work you need to have the dataset csv files in the molgpt folder (really in the directory where you run the scripts from). You can run for example this command:


```
python generate/generate.py --model_weight /content/molgpt/gua_tpsa_logp_sas.pt --props tpsa logp sas --data_name guacamol2 --csv_name gua_tpsa_temp1 --gen_size 1000 --batch_size 512 --vocab_size 94 --block_size 100
```
where model_weight is the path to the saved model weights and props tells the model which properties to condition on. If the model has been trained on a property it has to be included in the props otherwise there is an error with shapes mismatching. I have included some of the weights from kaggle in the weights folder. 

The generated smiles are exported to a csv file.

These files also contain some example commands of how to generate.
```
./generate_guacamol_prop.sh
```

```
./generate_moses_prop_scaf.sh
```

If you find this work useful, please cite:

Bagal, Viraj; Aggarwal, Rishal; Vinod, P. K.; Priyakumar, U. Deva (2021): MolGPT: Molecular Generation using a Transformer-Decoder Model. ChemRxiv. Preprint. https://doi.org/10.26434/chemrxiv.14561901.v1 


