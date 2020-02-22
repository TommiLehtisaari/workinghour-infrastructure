# Working Hours - Infrastructure

This is a little experimental repository in a step towards [GitOps](https://www.weave.works/technologies/gitops/), the modern way to do DevOps with containers by WeaveWorks. 

At the moment this does not do GitOps kind of delivery nor does it use kubernetes. The aim is to do GitOps with weaveworks tool [Flux](https://www.weave.works/oss/flux/) which is installed in a kubernetes cluster to provide Continuous Delivery on new pushes to DockerHub/GitHub.

For now this can be used as developper tool to view and test the Working Hour app itself. This can be done with a help of `docker-compose`.

#### Deploy the app with compose on this repo:

```bash
docker-compose up -d
```

The application can be viewed now on `localhost:3000`and Graphql API can be found from `localhost:4000/graphql`.


#### The app can be taken down on this repo:

```bash
docker-compose down
```