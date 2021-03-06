# Canadian Centre for Cyber Security

## CCCS YARA Specification

The [CCCS YARA Specification](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara.yml) has been created to define and validate the style and format of YARA rule metadata. 

Over the years we have seen many Yara rules; in order to leverage them to their full potential we always had to modify some of their associated metadata, even for rules we developped ourselves. Adjusting simple elements such as datetime format and adding important information to help analysts.

This specification also include fields specific to the [MITRE ATT&CK framework](https://attack.mitre.org/matrices/enterprise/) to identify techniques and universal [MITRE ATT&CK threat groups](https://attack.mitre.org/groups/).

Note: The [Cyber Threat Intelligence Repository](https://github.com/mitre/cti) is a submodule of this repository, "git clone --recurse-submodules https://github.com/CybercentreCanada/CCCS-Yara.git".

[AssemblyLine](https://www.cyber.gc.ca/en/assemblyline) supports this specification natively and will leverage it to provide more context around YARA signature hits.

## Components

yara_validator.py:		This is the validator library. It is used to verify specified the yara rule has specified metadata information, autogenerates some of the tags and sorts the tags in the canonical order with all 'unknown' metadata information appended to the bottom.

- [CCCS_Yara.yml](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara.yml):        This is the definition of the CCCS YARA Standard in the .yml format. (Limitation: This file is provided to show what fields are expected, currently the yara_validator dosen't use this file directly, this will be addressed in a future release.)

- [CCCS_Yara_values.yml](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara_values.yml): File which describe the list of acceptable values for fields defined in the CCCS_Yara.yml

yara_validator_cli.py:	This is a command line interface utility. It takes a file, list of files, a folder looking for files with the .yar or .yara extention. 

Note: the library and the cli are currently designed with the assumption that each file has a single yara rule in it.

# Centre canadien pour la cybersécurité

## Spécification YARA du CCCS

La [Spécification YARA du CCCS](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara.yml) a été créé pour définir et validé le style et le format des attributs pour les règles YARA. 

Au fil des années nous avons vu beaucoup de régles Yara; mais pour pouvoir les utilisées à leur plein potentiel nous devions modifiée les méta données associtiées, parfois même pour nos propres règles. En ajustant des éléments aussi simples que le format de date et en ajoutant des attributs important pour les analystes.

Ce standard pour les méta données inclus aussi des champs spécifique au [MITRE ATT&CK framework](https://attack.mitre.org/matrices/enterprise/) pour identifier les techniques et les groups d'acteurs [MITRE ATT&CK threat groups](https://attack.mitre.org/groups/).

[AssemblyLine](https://www.cyber.gc.ca/en/assemblyline) supporte cette spécification nativement et l'utilisera pour fournir d'avantage d'information à l'utilisateur lors du déclanchement d'une signature.

## Composantes

yara_validator.py:		La librairie de validation. Elle permet de vérifier si une règle YARA a tous les attributs nécessaires, elle auto-génère aussi certain attribut et les ordonnent selon l'ontologie. Tous les attributs supplémentaires ne faisant pas partie de la spécification sont placé à la fin.

- [CCCS_Yara.yml](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara.yml):        Fichier de de définition de la spécification. (Limitation: Ce fichier démontre les attributs nécessaires, présentement le validateur n'utilise pas se fichier directement, ceci sera améliorer dans le futur.)

- [CCCS_Yara_values.yml](https://github.com/CybercentreCanada/CCCS-YARA-Validator/blob/master/CCCS_Yara_values.yml): Fichier qui décrit les valeurs acceptables pour chacun des attributs définit dans CCCS_Yara.yml.

yara_validator_cli.py:	Utilitaire de validation pour la ligne de commande. Il accepte une règle, une liste de règles ou un dossier pour validé les fichiers se terminant par .yar ou .yara.  

Note:  la librairie et l'utilitaire de ligne de commande n'accepte que les fichiers qui contient une seule règle par fichier.


## Requirements

Python 3.6

All required python packages are in the requirements.txt

## yara_validator_cli.py usage

```
yara_validator_cli.py -h 
     ____ ____ ____ ____   __   __ _    ____      _    
    / ___/ ___/ ___/ ___|  \ \ / // \  |  _ \    / \   
   | |  | |  | |   \___ \   \ V // _ \ | |_) |  / _ \  
   | |__| |__| |___ ___) |   | |/ ___ \|  _ <  / ___ \ 
    \____\____\____|____/    |_/_/   \_\_| \_\/_/   \_\ 
    
usage: yara_validator_cli.py [-h] [-r] [-n] [-v] [-vv] [-f] [-w] [-s]
                             [-i | -c]
                             paths [paths ...]

CCCS YARA script to run the CCCS YARA validator, if the -i or -c flags are not
provided no changes will be made to the files.

positional arguments:
  paths                A list of files or folders to be analyzed.

optional arguments:
  -h, --help           show this help message and exit
  -r, --recursive      Recursively search folders provided.
  -n, --no-changes     Makes no changes and outputs potential results to the
                       output.
  -v, --verbose        Verbose mode, will print why a rule was invalid.
  -vv, --very-verbose  Very-verbose mode, will printout what rule is about to
                       be processed, the invalid rules, the reasons they are
                       invalid and all contents of the rule.
  -f, --fail           Fail mode, only prints messages about invalid rules.
  -w, --warnings       This mode will ignore warnings and proceed with other
                       behaviors if the rule is valid.
  -s, --standard       This prints the yara standard to the screen.
  -i, --in-place       Modifies valid files in place, mutually exclusive with
                       -c.
  -c, --create-files   Writes a new file for each valid file, mutually
                       exclusive with -i.
  ```
