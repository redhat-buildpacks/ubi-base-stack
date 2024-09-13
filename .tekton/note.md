## Commands to be executed to generate the pipelineRun

- Install and build the Quarkus application: 
```bash
git clone https://github.com/ch007m/pipeline-dsl-builder.git
cd pipeline-dsl-builder
./mvnw package
```

- Set the path to directory where the jar has been build
```bash
QUARKUS_DIR=$HOME/<PATH_TO>/pipeline-dsl-builder/builder/target/quarkus-app/
```

- Create the tmp directory where files are generated and tasks extracted
```bash
mkdir -p .tekton/out/flows/konflux
```

- Generate the pipelineRun for Konflux
```bash
cd .tekton
rm -rf out/flows/konflux
java -jar $QUARKUS_DIR/quarkus-run.jar builder \
  -c pipeline-generator-cfg.yaml \
  -o out/flows
  
cp out/flows/konflux/remote-build/pipelinerun-ubi-base-stack.yaml .
```
