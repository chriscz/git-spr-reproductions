# Steps
1. Clone a empty git repository with whatever name here, called for example `spr-test-repo`, with 
  - branch `main`
  - origin set
2. Add and commit `.spr.yml` as provided in `spr.yml` (updating your details as needed)
3. `git push origin main --set-upstream`
4. Now you are ready to run the script
5. `bin/main spr-test-repo`
6. Note error:
```
... previous output...
+ git spr update
> git rev-parse --show-toplevel
> git fetch
> git rebase origin/main --autostash
> github fetch pull requests
> git log --format=medium --no-color origin/main..HEAD
> git branch --no-color
> git log --format=medium --no-color origin/main..HEAD
> github update 30 : Add A [feat/2025-03-22_10-33-29]
> git status --porcelain --untracked-files=no
> git push --force --atomic origin 6ecca9412e8b8bfb8140a81613831c218db49091:refs/heads/spr/main/aa288f12 7d556aff3f0305eb27a2c213bcf9cc33f44c178c:refs/heads/spr/main/2bffd247 dec3347e1c9f52a8b0fa022348a97ed6842928cf:refs/heads/spr/main/cb7ae678
> github create 33 : Add B [feat/2025-03-22_10-33-29]
panic: createPullRequest: A pull request already exists for chriscz:spr/main/2bffd247.


goroutine 1 [running]:
github.com/ejoffe/spr/github/githubclient.check({0xa41aa0, 0xc0003184c8})
        /home/chris/dev/1-projects/git-spr-bug-reproduction/spr/github/githubclient/client.go:698 +0xf4
github.com/ejoffe/spr/github/githubclient.(*client).CreatePullRequest(0xc00011ea80, {0xa45d40, 0xdf8a20}, {0xa45c60, 0xc00011ea50}, 0xc00016e730, {{0xc000250182, 0x8}, {0xc0002500cd, 0x28}, ...}, ...)
        /home/chris/dev/1-projects/git-spr-bug-reproduction/spr/github/githubclient/client.go:406 +0x599
github.com/ejoffe/spr/spr.(*stackediff).UpdatePullRequests(0xc0002540e0, {0xa45d40, 0xdf8a20}, {0xdf8a20, 0x0, 0x0}, 0x0)
        /home/chris/dev/1-projects/git-spr-bug-reproduction/spr/spr/spr.go:222 +0xf43
main.main.func4(0xc000135700)
        /home/chris/dev/1-projects/git-spr-bug-reproduction/spr/cmd/spr/main.go:161 +0x10f
github.com/urfave/cli/v2.(*Command).Run(0xc00023d0e0, 0xc000135480)
        /home/chris/.local/opt/go/pkg/mod/github.com/urfave/cli/v2@v2.8.1/command.go:169 +0x5d4
github.com/urfave/cli/v2.(*App).RunContext(0xc000128ea0, {0xa45d40, 0xdf8a20}, {0xc000126080, 0x2, 0x2})
        /home/chris/.local/opt/go/pkg/mod/github.com/urfave/cli/v2@v2.8.1/app.go:341 +0xb47
github.com/urfave/cli/v2.(*App).Run(...)
        /home/chris/.local/opt/go/pkg/mod/github.com/urfave/cli/v2@v2.8.1/app.go:247
main.main()
        /home/chris/dev/1-projects/git-spr-bug-reproduction/spr/cmd/spr/main.go:229 +0x1225
```
7. Running `git spr update` in the repository again will result in the original first commit "Add A" now being directly based on `main`

# Other Scripts
1. `bin/nuke` for removing all local and remote branches and resetting to the first commit on the main repository. Use `bin/nuke spr-test-repo`
2. `bin/reorder` is used to reorder the commits from commit order A, B, C to the new order B, C, A 
