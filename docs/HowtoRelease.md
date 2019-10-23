### set version number

Use a version that conforms to semantic versioning 2.0.

When releasing, update the `NEWS.md` file and (usually) all
`setup.py` files. Note the versioning scheme remark
in the toplevel `setup.py` file.

#### Version number
Originally fody-backend had been designed with sub-modules
that could potentially also be used separately.
Example how to change all version numbers:
```sh
grep -rl "^    version=" . | xargs sed -i 's/0.4.4.dev0/0.5.0.dev0/'
```

#### DEB packaging
You need to add an new entry to `debian/changelog` for releases.

When the version of fody compatible with the backend changed, also
update the dependency in `debian/control`.

### tag version number
example for v0.4.3:
```sh
git tag v0.4.3
git push origin v0.4.3
```

### build
(whatever is necessary, see toplevel Readme)

### set dev number again
In the mentioned files above, to something like `0.4.4-dev`.
