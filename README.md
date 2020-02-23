# Working Hours - Infrastructure

This is a little experimental repository in a step towards [GitOps](https://www.weave.works/technologies/gitops/), the modern way to do DevOps with containers by WeaveWorks. 

At the moment this does not do GitOps kind of delivery nor does it use kubernetes. The aim is to do GitOps with weaveworks tool [Flux](https://www.weave.works/oss/flux/) which is installed in a kubernetes cluster to provide Continuous Delivery on new pushes to DockerHub/GitHub.

For now this can be used as developper tool to view and test the Working Hour app itself. This can be done with a help of `docker-compose`.

### Set environmentvariables

An Environment variable has to be set for bcrypt for password hashing:

```bash
export JWT_SECRET=<secret-string>
```

#### Deploy the app with compose on this repo:

```bash
docker-compose up -d
```

The application can be viewed now on `localhost:3000`and Graphql API can be found from `localhost:4000/graphql`.


#### The app can be taken down on this repo:

```bash
docker-compose down
```

### About Front End

The Front End Docker Image has currently hardcoded API Endpoint for `localhost:4000`. This is because of React. The Front End Docker Image uses optimized production build which gets hardcoded value from `.env.production`file. If the API Endpoint has to be switched the Front End can be build again from the [frontend-repo](https://github.com/TommiLehtisaari/workinghour-frontend). Image from `docker-compose.yml` hasto be also changed accordingly.

### Docker volumes

This will crate named volume for presistent data:
`workinghours-infrastructure_mongo-db` and `workinghours-infrastructure_mongo-config`

This can be queried with:

```bash
$ docker volume ls
DRIVER              VOLUME NAME
local               workinghours-infrastructure_mongo-config
local               workinghours-infrastructure_mongo-db
```
And deleted:

```bash
$ docker volume rm \
workinghours-infrastructure_mongo-config \
workinghours-infrastructure_mongo-db
```

## Admin privileges

This project is created so that other admins can promote users to admins as well. All the admins are on same rank so that once an admin can not be depromoted. First admin can be done with naming the first user as `username=superuser`.

go to: `localhost:4000/graphql` and inset the query:

```graphql
mutation {
	createUser(
		username: "superuser"
		name: "Adminstrator"
		password: "<password>"
	){
		value
	}
}
```

Other options are manipulating directly the database.