1. `git clone git@github.com:alunbestor/Boxer.git`
2. `git checkout 64bit/master`
3. `git submodule --init --recursive`
4. Open Boxer.xcodeproj in XCode.
5. Build.
6. If everything is fine, go to `Project Navigator` then `Signing & Capabilities` panel and add account.
7. Go to `Edit Scheme...` and change Boxer from `Debug` to `Release`.
8. Build then copy the release build to `Applications` folder.