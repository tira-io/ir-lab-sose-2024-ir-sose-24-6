# IR Lab SoSe 2024: Retrieval Systems by ir-sose-24-6

This repository contains the retrieval systems of ir-sose-24-6. We will implement and evaluate retrieval systems for a corpus of scientific papers (title + abstracts) from the fields of information retrieval and natural language processing (the [IR Anthology](https://ir.webis.de/anthology/) and the [ACL Anthology](https://aclanthology.org/)). We will use [TIRA](https://www.tira.io/) to evaluate the retrieval systems on a set of datasets. The evaluation is done in a controlled environment to improve reproducibility and comparability of the results.

We recommend that you work either in Github Codespaces or using [dev containers with Docker](https://code.visualstudio.com/docs/devcontainers/containers). Github Codespaces are an easy option to start in a few minutes (free tier of 130 CPU hours per month), whereas dev container with Docker might be interesting if you want to put a bit more focus on technical/deployment details.

## Repository Structure

If you try out diverse retrieval approach, try to develop each approach self-contained in a directory within this repository. See the `baseline-retrieval-system` directory for an example.

The `baseline-retrieval-system` example contains a single Jupyter notebook  file `baseline-retrieval-system.ipynb` that implements retrieval with BM25 with default parameters (i.e., no advanced document/query processing and also no fine-tuned retrieval pipeline). If you want to use additional dependencies or libraries, please add them to the `Dockerfile` (if you modify the Dockerfile, please rebuild the dev container).

A self-contained submission can then be submitted to TIRA using GitHub actions. See the [submitting your retrieval system](#submitting-your-retrieval-systems) section for more details.

## Developing your Retrieval System

You have two options for developing your submission. Either you can develop remotely in Github Codespaces or locally in a dev container.

### Developing in Github Codespaces

Click the `Code` button at the top of the repository and select `Open with Codespaces`. This will open a new Codespace with the repository loaded. You can then start developing your submission in the Codespace.

Additional information on how to use Github Codespaces can be found [here](https://docs.github.com/en/codespaces/).

### Developing in Dev Containers

A dev container (please find a suitable installation instruction [here](https://code.visualstudio.com/docs/devcontainers/containers)) allows you to directly work in the prepared Docker container so that you do not have to install the dependencies (which can sometimes be a bit tricky).

To develop with dev containers, please:

- Install [VS Code](https://code.visualstudio.com/download) and [Docker](https://docs.docker.com/engine/install/) on your machine
- Install the [Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VS Code
- Clone this repository: `git clone ...`
- Open the repository with VS Code (it should ask you to open the repository in a dev container)

## Submitting Your Retrieval System(s)

Run the github action to submit your software. Select the Action tab and then select `Upload Docker Software to TIRA` from the list of workflows on the left. Select the `Run workflow` button and input the path to the Jupyter notebook that implements your retrieval approach and clich on `Run workflow`. The Github action will build the docker image, test that the software works on a small input example, and then uploads the the image to TIRA where you can then run it on larger datasets (and on larger hardware resources, e.g., with a GPU).

## Running Your Retrieval System(s)

After sucessfully submitting your software by executing the Github Action, it will be avaiable on TIRA. Select `Submit` and then the `Docker` tab. Your software submission will be listed under the `Choose sofware ...` dropdown menu (the names are generated by docker, check the output of the github action to see which name corresponds to which submission). Select your submission and then select the resources (small will usually suffice) and dataset you want to run it on. Click `Run` to run your software on the dataset.

You can check the progress of your submission by unfolding the `Running Processes` tab at the top.

## Additional Hints

Some additional advanced hints for developing your submission:

### Additional dependencies

If you require additional depenedencies, you can add them to the `Dockerfile`. Please rebuild the devcontainer (the `.devcontainer.json` points to the Dockerfile) to ensure that your development environment is update.

### Running/Testing your submission locally

You can test your submission locally (e.g., if you want to debug a problem in the Github action) directly via (please install `tira` via `pip3 install tira`, Docker, and Python >= 3.7 on your machine) the following command (please replace `{image-name}` with the name of the image you want to run):

```bash
tira-run \
    --input-dataset ir-lab-sose-2024/ir-acl-anthology-20240504-training \
    --image {image-name}
```

