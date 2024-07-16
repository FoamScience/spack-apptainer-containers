# Spack-powered Apptainer containers for OpenFOAM

The objective of this repo is to demonstrate how to use
[openfoam-apptainer-packaging](https://github.com/FoamScience/openfoam-apptainer-packaging)
to build OpenFOAM containers using minimal definition files that take
leverage of [spack](https://github.com/spack/spack) to be Linux-Distribution-agnostic. This is
done through loading custom definitions for base containers (FoamScience/openfoam-apptainer-packaging#4).

Here are your quick instructions to get started:
```bash
git clone https://github.com/FoamScience/openfoam-apptainer-packaging /tmp/tainers
git clone https://github.com/FoamScience/spack-apptainer-containers
cd spack-apptainer-containers
ansible-playbook /tmp/tainers/build.yaml --extra-vars "original_dir=$PWD" --extra-vars "@config.yaml"
# check containers/basic
```

For more detailed documentation, head to
[FoamScience/openfoam-apptainer-packaging/docs.md](https://github.com/FoamScience/openfoam-apptainer-packaging/blob/main/docs.md)

## Pros

- Lean and clean definition files
- Unified software loading workflow
- Great potential for easy cross Linux-Distribution packaging: Switching base distros is (should be)
  as easy as changing one configuration item

## Cons

- Strong coupling to the software versions Spack provides.
- Currently, encountering random errors when building the same definition files on top of different
  Linux distributions if build caches.
- Large-size containers and potentially slow building time in case binaries
  are not found in the build caches (e.g. OpenFOAM containers will be around 1GB in size, compared to 400MB if installed
  from distribution binary packages).
- Hides stuff from `docker scout`
