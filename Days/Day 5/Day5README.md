Day 5: Docker Multi-Stage Builds & Image Optimization

1. Docker Multi-Stage build
naming convention people use is Dockerfile.multi
It utilizes multiple ```FROM``` statements in one Dockerfile

We separate the build stage as some compilers, package managers, build tools, etc are not needed at runtime.  This lets you keep only the compiled artifacts

Another use case is **test isolation*  
you can run your test suite without touching your production image target at all

```FROM builder AS test```

```docker build --target test```



2. Compiled vs Interpreted languages