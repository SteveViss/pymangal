# pymangal

`pymangal` is a `python` module to interact with the `mangal` API. The
documentation is here: <http://pymangal.readthedocs.org/en/latest/>

[![Build Status](https://travis-ci.org/mangal-wg/pymangal.png?branch=master)](https://travis-ci.org/mangal-wg/pymangal) [![Coverage Status](https://coveralls.io/repos/mangal-wg/pymangal/badge.svg?branch=master&service=github)](https://coveralls.io/github/mangal-wg/pymangal?branch=master) [![codecov.io](http://codecov.io/github/mangal-wg/pymangal/coverage.svg?branch=master)](http://codecov.io/github/mangal-wg/pymangal?branch=master) [![Documentation Status](https://readthedocs.org/projects/pymangal/badge/?version=latest)](http://pymangal.readthedocs.org/en/latest/)

**ALL** numbered versions are pushed to PyPI, so you can at all time install with `pip install pymangal`.

# TODO list

In no particular order

- `networkx` export
- Automated handling of `related` fields (append `prefix`)
- `signUp` method

# Versionning

Follows [semantic versioning][semver]. The version is given in the
`__version__` variable of `pymangal`. Most important releases are tagged.

# Short tutorial

Contrary to the `rmangal` package, this module focuses on implementing a
minimal set of functions. it's a little less user-friendly, but easier to
maintain (and learn).

Dialogue with the API is handled by an instance of the `mangal` class. The
four most important functions are `List`, `Get`, `Post`, and `Patch` (to,
respectively, see a list of data, get a particular record, add new data,
and patch them).

*Unlike in the R package*, there is a validation of the data done automatically
before the data are either posted or patched.

## Setting up

```python
import pymangal
# We create an instance of the mangal class
db = pymangal.mangal()
# Arguments: url, usr, pwd
```

## Reading data

```python
# Returns the first 20 datasets
db.List('dataset')

# Returns all datasets
db.List('dataset', page='all')

# Returns all taxa matching *vulgaris
db.List('taxa', filters='name__endswith=vulgaris', page='all')

# Get the first network
db.get('network', 1)
```

## Uploading data

```python
# Objects are represented as dict
taxa = {'name': 'Pisaster ochraceus', 'vernacular': 'purple sea star',
        'status': 'confirmed', 'eol': '598469'}
# You need to have a username/API key to add and patch objects
db_auth = pymangal.mangal(usr='test', key='dsdsdsdsdsds')
taxa = db_auth.Post('taxa', taxa)
print taxa['id']
```

[ls]: http://sphinx-doc.org/intro.html
[semver]: http://semver.org/
