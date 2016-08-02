# bagtainers

[![Build Status](https://travis-ci.org/o2r-project/bagtainers.svg?branch=master)](https://travis-ci.org/o2r-project/bagtainers)

Bagtainers drafts can be found in numbered subdirectories (ordered by creation date). The documentation of each level of the development is  in the file `INDEX.md`.

## Tools

### Uploader container

A container to upload example bagtainers to an implementation of the [o2r api](http://o2r.info/o2r-web-api) can be build and run with the following commands:

```bash
# optinal: build and tag locally
# docker build -t examplecompendia .

docker run --rm  o2rproject/examplecompendia -e 1
# note the returned ID
curl http://172.17.0.1/api/v1/compendium/<compendium ID> | python -mjson.tool

# upload 7 examples and selected bagtainers to a specific API endpoint 
docker run --rm o2rproject/examplecompendia -a http://192.168.0.0:8088/api/v1/compendium -e 7 -b 0003 -b 0004 -b 0005
```

It can be used to upload multiple test compendia from o2r-muncher or selected bagtainers from this repository.

**Parameters**

- `-e <n>`: upload n-many test compendia, e.g. `-e 42`
- `-b XXXX`: upload specific examples, based on directory name, e.g. `-b 0003`
  - can be used multiple times, e.g. `-b 0003 -b 0005`
- `-a http://...`: the API endpoint, by default it is the local docker host IP: `http://172.17.0.1/api/v1/compendium`
- `-k <key>`: the API upload key, default is `CHANGE_ME`

Once the compendia are uploaded, you can start jobs:

```bash
curl -F compendium_id=<compendium ID> http://172.17.0.1/api/v1/job
# note the returned job ID
curl http://172.17.0.1/api/v1/job/<job ID> | python -mjson.tool
```

### Directory listings

The file `dirtree.pl` is a little Perl script by Arjen Bax (via [texblog](http://texblog.org/2012/08/07/semi-automatic-directory-tree-in-latex/#comment-5396) to create directory listings for the LaTeX package [dirtree](http://tug.ctan.org/macros/generic/dirtree/).

```bash
perl dirtree.pl path/to/directory
```

## License

The bagtainers in this directory are all published under copyrights by the respective content authors.
