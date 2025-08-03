```
check CONTRIBUTING.md for rules for contributions
```

```
#quick local launch

git clone https://github.com/amv-ui/docs
cd docs/docs/source

echo "alias runDocs='sphinx-autobuild . _build/html'" >> ~/.bashrc
source ~/.bashrc
runDocs
```

```
#how to add documentation?
#all documentation will be compiled on docs/source/*.rst
#for example index.rst and usage.rst
```

reference: <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html>
