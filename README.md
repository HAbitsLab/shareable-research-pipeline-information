# shareable-research-pipeline-information
A space to share information and standards for making research code and data shareable. The goal is to think about this information during the design and development of the project so make the process of sharing the research code easier with publications. 

The tools and design choices during the development of research projects can help to make the code and data easier to understand and share.

> The deliverables of a sharable project is to provide a framework to go from raw data to the figures and tables reported in the publications


## Github file structure
> This is the general structure convention for github repos. This might not fit every project that comes up but the general structure of 
```bash
├── code
│   └── README.md
├── data
│   └── README.md
├── docs
├── README.md
└── .gitignore
```
> Deeper example:

```bash
├── code
│   ├── main-project-code
│   │   ├── main-project-code.py
│   │   ├── README.md
│   ├── preprocessing-code
│   │   ├── preprocessing-code.py
│   ├── shell-scripts
│   │   ├── run-main-process-script.sh
│   │   ├── preprocess-shell-script.sh
│   └── README.md
├── data
│   ├── participant-data
│   │   ├── participant-id-1
│   │   │   ├──device-id-1
│   │   │   │   ├──p1-device-data.csv
│   │   ├── participant-id-2
│   │   │   ├──device-id-1
│   │   │   │   ├──p2-device-data.csv
│   └── README.md
├── docs
│   ├── images
│   │   ├── figure-1.png
│   │   ├── figure-2.png
│   │   ├── figure-3.png
│   ├── publication.pdf
│   └── README.md
├── README.md
└── .gitignore
```
> The exact structure might vary, but the researcher must be able to explain where the raw data and code are and how to transform and transport that data through the pipeline. 

The [README.md](README.md) file in the root directory should provide the high-level view and running of the project. It is possible to have a README in each sub-directory as well. This might be useful if you need to provide a more in-depth explanation of an algorithm or equation.

## Flow of data

!["shareable research diagram"](docs\images\shareable-research-diagram.png "shareable research diagram")
> The focus for the shareable code as data is the figure outlined in blue/ Moving from de-identified raw data to the output of publication figures and tables.

## Questions to thing about when designing project repository and writing the README:
### RAW DATA
1. What is the raw data in the pipeline?
    - How was it collected( survey, device, sensor array, etc)?
        - Link to another github project to go into greater detail about the device
        - Link to device data sheet
        - Link to device website 
    - Describe the data?
        - Are there multiple files for each participant? 
        - Filetype
        - What are labels?
        - What are units?
        - Frequency of collection
        - Etc.
        - If lots of fields or sensors can generally describe the groups of collected data points.
    - Where is data available?
        - Is it located in the github repo or Zenodo page?
            - Use a [a relative link](data) if it is inside the repo
            - Use outside URL ([ex. Zenodo link](https://zenodo.org/)) if in other data sharing service

### PREPROCESSING
2. Was preprocessing used to clean the data?
    - What methods were used to clean the data
        - Resampling, smoothing, etc?
    - Why was this done?
    - Is the preprocessed clean data available?
        - Links to the cleaned data
     or must the researchers go through the preprocessing steps?
    - If preprocessing is necessary, clearly define those steps with either links to code or commands to run

### PROCESSING
3. What are main processing steps?
    - Is there an order to these steps?
    - Shell script to run?
        - Still explain an overview of the steps used in the main algorithms to process the data. 
    - Are there parameters that need to be set or can be changed to produce different results
    - Can link to READMEs in the sub-dirs that explain more in-depth

### OUTPUT
4. Describe the output data.
    - Are there multiple output sets from the processing step?
    - How to produce figures and tables used in the publication from these sets
        - Links to figure in docs directory for comparison?

## How to Run
Explain how to run the code to flow through the data pipeline. This should be OS agnostic, but some code might need to be refactored in order to make this possible. If it will only run on a single OS, that is a limitation, but state clearly in the README to avoid confusion and issues being raised with the code.

- Explain environment
    - Ex. Python 2 vs 3.
    - Do environment variables need to be set?

> The 3 main issues with troubleshooting code portability are: **Permissions, Paths, and Dependencies**.

Possible issues:
- Permissions
    - Do any shell scripts require ```chmod``` to run?
- Path
    - Are the paths hardcoded?
- Dependencies
    - Include any dependency requirements
        - With python/pip you can add [requirements.txt](https://pip.pypa.io/en/stable/user_guide/#requirements-files)

## Paths
In order to make the code portable, try to not hard-code any directory paths. This might be a challenge as the developer might specify paths for data in algorithms, but try to use the environment, config files, or command line arguments. 

## Public Data and Code Concerns
In making data and code public it is important to make the code reusable and sharable without exposing vulnerabilities.
- **DO NOT SHARE ANY IDENTIFIABLE PARTICIPANT DATA!**
- Do not hard-code any **API TOKENS** or **CONNECTION STRINGS** or any other keys that can be used to access accounts.
- If this information is needed to run the code, either use Environment variables or a config/setting file (ex. config.py) and add that file to the [.gitignore file](https://git-scm.com/docs/gitignore).
    - Clearly state in the README that these variables need to be added by the user in order to make code usable.

## Future Portability of Code and Data
Docker image build to include data and code in a container. For easier reproducibility of project.
