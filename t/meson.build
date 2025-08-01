clar_test_suites = [
  'unit-tests/u-ctype.c',
  'unit-tests/u-example-decorate.c',
  'unit-tests/u-hash.c',
  'unit-tests/u-hashmap.c',
  'unit-tests/u-mem-pool.c',
  'unit-tests/u-oid-array.c',
  'unit-tests/u-oidmap.c',
  'unit-tests/u-oidtree.c',
  'unit-tests/u-prio-queue.c',
  'unit-tests/u-reftable-tree.c',
  'unit-tests/u-strbuf.c',
  'unit-tests/u-strcmp-offset.c',
  'unit-tests/u-string-list.c',
  'unit-tests/u-strvec.c',
  'unit-tests/u-trailer.c',
  'unit-tests/u-urlmatch-normalization.c',
]

clar_sources = [
  'unit-tests/clar/clar.c',
  'unit-tests/unit-test.c',
  'unit-tests/lib-oid.c'
]

clar_decls_h = custom_target(
  input: clar_test_suites,
  output: 'clar-decls.h',
  command : [
    shell,
    meson.current_source_dir() + '/unit-tests/generate-clar-decls.sh',
    '@OUTPUT@',
    '@INPUT@',
  ],
  env: script_environment,
)
clar_sources += clar_decls_h

clar_sources += custom_target(
  input: clar_decls_h,
  output: 'clar.suite',
  command : [
    shell,
    meson.current_source_dir() + '/unit-tests/generate-clar-suites.sh',
    '@INPUT@',
    '@OUTPUT@',
  ],
  env: script_environment,
)

clar_unit_tests = executable('unit-tests',
  sources: clar_sources + clar_test_suites,
  dependencies: [libgit_commonmain],
)
test('unit-tests', clar_unit_tests, kwargs: test_kwargs)

unit_test_programs = [
  'unit-tests/t-reftable-basics.c',
  'unit-tests/t-reftable-block.c',
  'unit-tests/t-reftable-merged.c',
  'unit-tests/t-reftable-pq.c',
  'unit-tests/t-reftable-readwrite.c',
  'unit-tests/t-reftable-record.c',
  'unit-tests/t-reftable-stack.c',
  'unit-tests/t-reftable-table.c',
]

foreach unit_test_program : unit_test_programs
  unit_test_name = fs.stem(unit_test_program)
  unit_test = executable(unit_test_name,
    sources: [
      'unit-tests/test-lib.c',
      'unit-tests/lib-reftable.c',
      unit_test_program,
    ],
    dependencies: [libgit_commonmain],
  )
  test(unit_test_name, unit_test,
    workdir: meson.current_source_dir(),
    kwargs: test_kwargs,
  )
endforeach

subdir('helper')

integration_tests = [
  't0000-basic.sh',
  't0001-init.sh',
  't0002-gitfile.sh',
  't0003-attributes.sh',
  't0004-unwritable.sh',
  't0005-signals.sh',
  't0006-date.sh',
  't0007-git-var.sh',
  't0008-ignores.sh',
  't0010-racy-git.sh',
  't0012-help.sh',
  't0013-sha1dc.sh',
  't0014-alias.sh',
  't0017-env-helper.sh',
  't0018-advice.sh',
  't0019-json-writer.sh',
  't0020-crlf.sh',
  't0021-conversion.sh',
  't0022-crlf-rename.sh',
  't0023-crlf-am.sh',
  't0024-crlf-archive.sh',
  't0025-crlf-renormalize.sh',
  't0026-eol-config.sh',
  't0027-auto-crlf.sh',
  't0028-working-tree-encoding.sh',
  't0029-core-unsetenvvars.sh',
  't0030-stripspace.sh',
  't0033-safe-directory.sh',
  't0034-root-safe-directory.sh',
  't0035-safe-bare-repository.sh',
  't0040-parse-options.sh',
  't0041-usage.sh',
  't0050-filesystem.sh',
  't0051-windows-named-pipe.sh',
  't0052-simple-ipc.sh',
  't0055-beyond-symlinks.sh',
  't0056-git-C.sh',
  't0060-path-utils.sh',
  't0061-run-command.sh',
  't0062-revision-walking.sh',
  't0066-dir-iterator.sh',
  't0067-parse_pathspec_file.sh',
  't0068-for-each-repo.sh',
  't0070-fundamental.sh',
  't0071-sort.sh',
  't0080-unit-test-output.sh',
  't0081-find-pack.sh',
  't0090-cache-tree.sh',
  't0091-bugreport.sh',
  't0092-diagnose.sh',
  't0095-bloom.sh',
  't0100-previous.sh',
  't0101-at-syntax.sh',
  't0200-gettext-basic.sh',
  't0201-gettext-fallbacks.sh',
  't0202-gettext-perl.sh',
  't0203-gettext-setlocale-sanity.sh',
  't0204-gettext-reencode-sanity.sh',
  't0210-trace2-normal.sh',
  't0211-trace2-perf.sh',
  't0212-trace2-event.sh',
  't0300-credentials.sh',
  't0301-credential-cache.sh',
  't0302-credential-store.sh',
  't0303-credential-external.sh',
  't0410-partial-clone.sh',
  't0411-clone-from-partial.sh',
  't0450-txt-doc-vs-help.sh',
  't0500-progress-display.sh',
  't0600-reffiles-backend.sh',
  't0601-reffiles-pack-refs.sh',
  't0602-reffiles-fsck.sh',
  't0610-reftable-basics.sh',
  't0611-reftable-httpd.sh',
  't0612-reftable-jgit-compatibility.sh',
  't0613-reftable-write-options.sh',
  't1000-read-tree-m-3way.sh',
  't1001-read-tree-m-2way.sh',
  't1002-read-tree-m-u-2way.sh',
  't1003-read-tree-prefix.sh',
  't1004-read-tree-m-u-wf.sh',
  't1005-read-tree-reset.sh',
  't1006-cat-file.sh',
  't1007-hash-object.sh',
  't1008-read-tree-overlay.sh',
  't1009-read-tree-new-index.sh',
  't1010-mktree.sh',
  't1011-read-tree-sparse-checkout.sh',
  't1012-read-tree-df.sh',
  't1013-read-tree-submodule.sh',
  't1014-read-tree-confusing.sh',
  't1015-read-index-unmerged.sh',
  't1016-compatObjectFormat.sh',
  't1020-subdirectory.sh',
  't1022-read-tree-partial-clone.sh',
  't1050-large.sh',
  't1051-large-conversion.sh',
  't1060-object-corruption.sh',
  't1090-sparse-checkout-scope.sh',
  't1091-sparse-checkout-builtin.sh',
  't1092-sparse-checkout-compatibility.sh',
  't1100-commit-tree-options.sh',
  't1300-config.sh',
  't1301-shared-repo.sh',
  't1302-repo-version.sh',
  't1303-wacky-config.sh',
  't1304-default-acl.sh',
  't1305-config-include.sh',
  't1306-xdg-files.sh',
  't1307-config-blob.sh',
  't1308-config-set.sh',
  't1309-early-config.sh',
  't1310-config-default.sh',
  't1350-config-hooks-path.sh',
  't1400-update-ref.sh',
  't1401-symbolic-ref.sh',
  't1402-check-ref-format.sh',
  't1403-show-ref.sh',
  't1404-update-ref-errors.sh',
  't1405-main-ref-store.sh',
  't1406-submodule-ref-store.sh',
  't1407-worktree-ref-store.sh',
  't1408-packed-refs.sh',
  't1409-avoid-packing-refs.sh',
  't1410-reflog.sh',
  't1411-reflog-show.sh',
  't1412-reflog-loop.sh',
  't1413-reflog-detach.sh',
  't1414-reflog-walk.sh',
  't1415-worktree-refs.sh',
  't1416-ref-transaction-hooks.sh',
  't1417-reflog-updateref.sh',
  't1418-reflog-exists.sh',
  't1419-exclude-refs.sh',
  't1420-lost-found.sh',
  't1430-bad-ref-name.sh',
  't1450-fsck.sh',
  't1451-fsck-buffer.sh',
  't1460-refs-migrate.sh',
  't1500-rev-parse.sh',
  't1501-work-tree.sh',
  't1502-rev-parse-parseopt.sh',
  't1503-rev-parse-verify.sh',
  't1504-ceiling-dirs.sh',
  't1505-rev-parse-last.sh',
  't1506-rev-parse-diagnosis.sh',
  't1507-rev-parse-upstream.sh',
  't1508-at-combinations.sh',
  't1509-root-work-tree.sh',
  't1510-repo-setup.sh',
  't1511-rev-parse-caret.sh',
  't1512-rev-parse-disambiguation.sh',
  't1513-rev-parse-prefix.sh',
  't1514-rev-parse-push.sh',
  't1515-rev-parse-outside-repo.sh',
  't1517-outside-repo.sh',
  't1600-index.sh',
  't1601-index-bogus.sh',
  't1700-split-index.sh',
  't1701-racy-split-index.sh',
  't1800-hook.sh',
  't2000-conflict-when-checking-files-out.sh',
  't2002-checkout-cache-u.sh',
  't2003-checkout-cache-mkdir.sh',
  't2004-checkout-cache-temp.sh',
  't2005-checkout-index-symlinks.sh',
  't2006-checkout-index-basic.sh',
  't2007-checkout-symlink.sh',
  't2008-checkout-subdir.sh',
  't2009-checkout-statinfo.sh',
  't2010-checkout-ambiguous.sh',
  't2011-checkout-invalid-head.sh',
  't2012-checkout-last.sh',
  't2013-checkout-submodule.sh',
  't2014-checkout-switch.sh',
  't2015-checkout-unborn.sh',
  't2016-checkout-patch.sh',
  't2017-checkout-orphan.sh',
  't2018-checkout-branch.sh',
  't2019-checkout-ambiguous-ref.sh',
  't2020-checkout-detach.sh',
  't2021-checkout-overwrite.sh',
  't2022-checkout-paths.sh',
  't2023-checkout-m.sh',
  't2024-checkout-dwim.sh',
  't2025-checkout-no-overlay.sh',
  't2026-checkout-pathspec-file.sh',
  't2027-checkout-track.sh',
  't2030-unresolve-info.sh',
  't2050-git-dir-relative.sh',
  't2060-switch.sh',
  't2070-restore.sh',
  't2071-restore-patch.sh',
  't2072-restore-pathspec-file.sh',
  't2080-parallel-checkout-basics.sh',
  't2081-parallel-checkout-collisions.sh',
  't2082-parallel-checkout-attributes.sh',
  't2100-update-cache-badpath.sh',
  't2101-update-index-reupdate.sh',
  't2102-update-index-symlinks.sh',
  't2103-update-index-ignore-missing.sh',
  't2104-update-index-skip-worktree.sh',
  't2105-update-index-gitfile.sh',
  't2106-update-index-assume-unchanged.sh',
  't2107-update-index-basic.sh',
  't2108-update-index-refresh-racy.sh',
  't2200-add-update.sh',
  't2201-add-update-typechange.sh',
  't2202-add-addremove.sh',
  't2203-add-intent.sh',
  't2204-add-ignored.sh',
  't2205-add-worktree-config.sh',
  't2300-cd-to-toplevel.sh',
  't2400-worktree-add.sh',
  't2401-worktree-prune.sh',
  't2402-worktree-list.sh',
  't2403-worktree-move.sh',
  't2404-worktree-config.sh',
  't2405-worktree-submodule.sh',
  't2406-worktree-repair.sh',
  't2407-worktree-heads.sh',
  't2500-untracked-overwriting.sh',
  't2501-cwd-empty.sh',
  't3000-ls-files-others.sh',
  't3001-ls-files-others-exclude.sh',
  't3002-ls-files-dashpath.sh',
  't3003-ls-files-exclude.sh',
  't3004-ls-files-basic.sh',
  't3005-ls-files-relative.sh',
  't3006-ls-files-long.sh',
  't3007-ls-files-recurse-submodules.sh',
  't3008-ls-files-lazy-init-name-hash.sh',
  't3009-ls-files-others-nonsubmodule.sh',
  't3010-ls-files-killed-modified.sh',
  't3011-common-prefixes-and-directory-traversal.sh',
  't3012-ls-files-dedup.sh',
  't3013-ls-files-format.sh',
  't3020-ls-files-error-unmatch.sh',
  't3040-subprojects-basic.sh',
  't3050-subprojects-fetch.sh',
  't3060-ls-files-with-tree.sh',
  't3070-wildmatch.sh',
  't3100-ls-tree-restrict.sh',
  't3101-ls-tree-dirname.sh',
  't3102-ls-tree-wildcards.sh',
  't3103-ls-tree-misc.sh',
  't3104-ls-tree-format.sh',
  't3105-ls-tree-output.sh',
  't3200-branch.sh',
  't3201-branch-contains.sh',
  't3202-show-branch.sh',
  't3203-branch-output.sh',
  't3204-branch-name-interpretation.sh',
  't3205-branch-color.sh',
  't3206-range-diff.sh',
  't3207-branch-submodule.sh',
  't3211-peel-ref.sh',
  't3300-funny-names.sh',
  't3301-notes.sh',
  't3302-notes-index-expensive.sh',
  't3303-notes-subtrees.sh',
  't3304-notes-mixed.sh',
  't3305-notes-fanout.sh',
  't3306-notes-prune.sh',
  't3307-notes-man.sh',
  't3308-notes-merge.sh',
  't3309-notes-merge-auto-resolve.sh',
  't3310-notes-merge-manual-resolve.sh',
  't3311-notes-merge-fanout.sh',
  't3320-notes-merge-worktrees.sh',
  't3321-notes-stripspace.sh',
  't3400-rebase.sh',
  't3401-rebase-and-am-rename.sh',
  't3402-rebase-merge.sh',
  't3403-rebase-skip.sh',
  't3404-rebase-interactive.sh',
  't3405-rebase-malformed.sh',
  't3406-rebase-message.sh',
  't3407-rebase-abort.sh',
  't3408-rebase-multi-line.sh',
  't3409-rebase-environ.sh',
  't3412-rebase-root.sh',
  't3413-rebase-hook.sh',
  't3415-rebase-autosquash.sh',
  't3416-rebase-onto-threedots.sh',
  't3417-rebase-whitespace-fix.sh',
  't3418-rebase-continue.sh',
  't3419-rebase-patch-id.sh',
  't3420-rebase-autostash.sh',
  't3421-rebase-topology-linear.sh',
  't3422-rebase-incompatible-options.sh',
  't3423-rebase-reword.sh',
  't3424-rebase-empty.sh',
  't3425-rebase-topology-merges.sh',
  't3426-rebase-submodule.sh',
  't3427-rebase-subtree.sh',
  't3428-rebase-signoff.sh',
  't3429-rebase-edit-todo.sh',
  't3430-rebase-merges.sh',
  't3431-rebase-fork-point.sh',
  't3432-rebase-fast-forward.sh',
  't3433-rebase-across-mode-change.sh',
  't3434-rebase-i18n.sh',
  't3435-rebase-gpg-sign.sh',
  't3436-rebase-more-options.sh',
  't3437-rebase-fixup-options.sh',
  't3438-rebase-broken-files.sh',
  't3500-cherry.sh',
  't3501-revert-cherry-pick.sh',
  't3502-cherry-pick-merge.sh',
  't3503-cherry-pick-root.sh',
  't3504-cherry-pick-rerere.sh',
  't3505-cherry-pick-empty.sh',
  't3506-cherry-pick-ff.sh',
  't3507-cherry-pick-conflict.sh',
  't3508-cherry-pick-many-commits.sh',
  't3509-cherry-pick-merge-df.sh',
  't3510-cherry-pick-sequence.sh',
  't3511-cherry-pick-x.sh',
  't3512-cherry-pick-submodule.sh',
  't3513-revert-submodule.sh',
  't3514-cherry-pick-revert-gpg.sh',
  't3600-rm.sh',
  't3601-rm-pathspec-file.sh',
  't3602-rm-sparse-checkout.sh',
  't3650-replay-basics.sh',
  't3700-add.sh',
  't3701-add-interactive.sh',
  't3702-add-edit.sh',
  't3703-add-magic-pathspec.sh',
  't3704-add-pathspec-file.sh',
  't3705-add-sparse-checkout.sh',
  't3800-mktag.sh',
  't3900-i18n-commit.sh',
  't3901-i18n-patch.sh',
  't3902-quoted.sh',
  't3903-stash.sh',
  't3904-stash-patch.sh',
  't3905-stash-include-untracked.sh',
  't3906-stash-submodule.sh',
  't3907-stash-show-config.sh',
  't3908-stash-in-worktree.sh',
  't3909-stash-pathspec-file.sh',
  't3910-mac-os-precompose.sh',
  't3920-crlf-messages.sh',
  't4000-diff-format.sh',
  't4001-diff-rename.sh',
  't4002-diff-basic.sh',
  't4003-diff-rename-1.sh',
  't4004-diff-rename-symlink.sh',
  't4005-diff-rename-2.sh',
  't4006-diff-mode.sh',
  't4007-rename-3.sh',
  't4008-diff-break-rewrite.sh',
  't4009-diff-rename-4.sh',
  't4010-diff-pathspec.sh',
  't4011-diff-symlink.sh',
  't4012-diff-binary.sh',
  't4013-diff-various.sh',
  't4014-format-patch.sh',
  't4015-diff-whitespace.sh',
  't4016-diff-quote.sh',
  't4017-diff-retval.sh',
  't4018-diff-funcname.sh',
  't4019-diff-wserror.sh',
  't4020-diff-external.sh',
  't4021-format-patch-numbered.sh',
  't4022-diff-rewrite.sh',
  't4023-diff-rename-typechange.sh',
  't4024-diff-optimize-common.sh',
  't4025-hunk-header.sh',
  't4026-color.sh',
  't4027-diff-submodule.sh',
  't4028-format-patch-mime-headers.sh',
  't4029-diff-trailing-space.sh',
  't4030-diff-textconv.sh',
  't4031-diff-rewrite-binary.sh',
  't4032-diff-inter-hunk-context.sh',
  't4033-diff-patience.sh',
  't4034-diff-words.sh',
  't4035-diff-quiet.sh',
  't4036-format-patch-signer-mime.sh',
  't4037-diff-r-t-dirs.sh',
  't4038-diff-combined.sh',
  't4039-diff-assume-unchanged.sh',
  't4040-whitespace-status.sh',
  't4041-diff-submodule-option.sh',
  't4042-diff-textconv-caching.sh',
  't4043-diff-rename-binary.sh',
  't4044-diff-index-unique-abbrev.sh',
  't4045-diff-relative.sh',
  't4046-diff-unmerged.sh',
  't4047-diff-dirstat.sh',
  't4048-diff-combined-binary.sh',
  't4049-diff-stat-count.sh',
  't4050-diff-histogram.sh',
  't4051-diff-function-context.sh',
  't4052-stat-output.sh',
  't4053-diff-no-index.sh',
  't4054-diff-bogus-tree.sh',
  't4055-diff-context.sh',
  't4056-diff-order.sh',
  't4057-diff-combined-paths.sh',
  't4058-diff-duplicates.sh',
  't4059-diff-submodule-not-initialized.sh',
  't4060-diff-submodule-option-diff-format.sh',
  't4061-diff-indent.sh',
  't4062-diff-pickaxe.sh',
  't4063-diff-blobs.sh',
  't4064-diff-oidfind.sh',
  't4065-diff-anchored.sh',
  't4066-diff-emit-delay.sh',
  't4067-diff-partial-clone.sh',
  't4068-diff-symmetric-merge-base.sh',
  't4069-remerge-diff.sh',
  't4070-diff-pairs.sh',
  't4071-diff-minimal.sh',
  't4100-apply-stat.sh',
  't4101-apply-nonl.sh',
  't4102-apply-rename.sh',
  't4103-apply-binary.sh',
  't4104-apply-boundary.sh',
  't4105-apply-fuzz.sh',
  't4106-apply-stdin.sh',
  't4107-apply-ignore-whitespace.sh',
  't4108-apply-threeway.sh',
  't4109-apply-multifrag.sh',
  't4110-apply-scan.sh',
  't4111-apply-subdir.sh',
  't4112-apply-renames.sh',
  't4113-apply-ending.sh',
  't4114-apply-typechange.sh',
  't4115-apply-symlink.sh',
  't4116-apply-reverse.sh',
  't4117-apply-reject.sh',
  't4118-apply-empty-context.sh',
  't4119-apply-config.sh',
  't4120-apply-popt.sh',
  't4121-apply-diffs.sh',
  't4122-apply-symlink-inside.sh',
  't4123-apply-shrink.sh',
  't4124-apply-ws-rule.sh',
  't4125-apply-ws-fuzz.sh',
  't4126-apply-empty.sh',
  't4127-apply-same-fn.sh',
  't4128-apply-root.sh',
  't4129-apply-samemode.sh',
  't4130-apply-criss-cross-rename.sh',
  't4131-apply-fake-ancestor.sh',
  't4132-apply-removal.sh',
  't4133-apply-filenames.sh',
  't4134-apply-submodule.sh',
  't4135-apply-weird-filenames.sh',
  't4136-apply-check.sh',
  't4137-apply-submodule.sh',
  't4138-apply-ws-expansion.sh',
  't4139-apply-escape.sh',
  't4140-apply-ita.sh',
  't4141-apply-too-large.sh',
  't4150-am.sh',
  't4151-am-abort.sh',
  't4152-am-subjects.sh',
  't4153-am-resume-override-opts.sh',
  't4200-rerere.sh',
  't4201-shortlog.sh',
  't4202-log.sh',
  't4203-mailmap.sh',
  't4204-patch-id.sh',
  't4205-log-pretty-formats.sh',
  't4206-log-follow-harder-copies.sh',
  't4207-log-decoration-colors.sh',
  't4208-log-magic-pathspec.sh',
  't4209-log-pickaxe.sh',
  't4210-log-i18n.sh',
  't4211-line-log.sh',
  't4212-log-corrupt.sh',
  't4213-log-tabexpand.sh',
  't4214-log-graph-octopus.sh',
  't4215-log-skewed-merges.sh',
  't4216-log-bloom.sh',
  't4217-log-limit.sh',
  't4252-am-options.sh',
  't4253-am-keep-cr-dos.sh',
  't4254-am-corrupt.sh',
  't4255-am-submodule.sh',
  't4256-am-format-flowed.sh',
  't4257-am-interactive.sh',
  't4258-am-quoted-cr.sh',
  't4300-merge-tree.sh',
  't4301-merge-tree-write-tree.sh',
  't5000-tar-tree.sh',
  't5001-archive-attr.sh',
  't5002-archive-attr-pattern.sh',
  't5003-archive-zip.sh',
  't5004-archive-corner-cases.sh',
  't5100-mailinfo.sh',
  't5150-request-pull.sh',
  't5200-update-server-info.sh',
  't5300-pack-object.sh',
  't5301-sliding-window.sh',
  't5302-pack-index.sh',
  't5303-pack-corruption-resilience.sh',
  't5304-prune.sh',
  't5305-include-tag.sh',
  't5306-pack-nobase.sh',
  't5307-pack-missing-commit.sh',
  't5308-pack-detect-duplicates.sh',
  't5309-pack-delta-cycles.sh',
  't5310-pack-bitmaps.sh',
  't5311-pack-bitmaps-shallow.sh',
  't5312-prune-corruption.sh',
  't5313-pack-bounds-checks.sh',
  't5314-pack-cycle-detection.sh',
  't5315-pack-objects-compression.sh',
  't5316-pack-delta-depth.sh',
  't5317-pack-objects-filter-objects.sh',
  't5318-commit-graph.sh',
  't5319-multi-pack-index.sh',
  't5320-delta-islands.sh',
  't5321-pack-large-objects.sh',
  't5322-pack-objects-sparse.sh',
  't5323-pack-redundant.sh',
  't5324-split-commit-graph.sh',
  't5325-reverse-index.sh',
  't5326-multi-pack-bitmaps.sh',
  't5327-multi-pack-bitmaps-rev.sh',
  't5328-commit-graph-64bit-time.sh',
  't5329-pack-objects-cruft.sh',
  't5330-no-lazy-fetch-with-commit-graph.sh',
  't5331-pack-objects-stdin.sh',
  't5332-multi-pack-reuse.sh',
  't5333-pseudo-merge-bitmaps.sh',
  't5334-incremental-multi-pack-index.sh',
  't5351-unpack-large-objects.sh',
  't5400-send-pack.sh',
  't5401-update-hooks.sh',
  't5402-post-merge-hook.sh',
  't5403-post-checkout-hook.sh',
  't5404-tracking-branches.sh',
  't5405-send-pack-rewind.sh',
  't5406-remote-rejects.sh',
  't5407-post-rewrite-hook.sh',
  't5408-send-pack-stdin.sh',
  't5409-colorize-remote-messages.sh',
  't5410-receive-pack.sh',
  't5411-proc-receive-hook.sh',
  't5500-fetch-pack.sh',
  't5501-fetch-push-alternates.sh',
  't5502-quickfetch.sh',
  't5503-tagfollow.sh',
  't5504-fetch-receive-strict.sh',
  't5505-remote.sh',
  't5506-remote-groups.sh',
  't5507-remote-environment.sh',
  't5509-fetch-push-namespaces.sh',
  't5510-fetch.sh',
  't5511-refspec.sh',
  't5512-ls-remote.sh',
  't5513-fetch-track.sh',
  't5514-fetch-multiple.sh',
  't5515-fetch-merge-logic.sh',
  't5516-fetch-push.sh',
  't5517-push-mirror.sh',
  't5518-fetch-exit-status.sh',
  't5519-push-alternates.sh',
  't5520-pull.sh',
  't5521-pull-options.sh',
  't5522-pull-symlink.sh',
  't5523-push-upstream.sh',
  't5524-pull-msg.sh',
  't5525-fetch-tagopt.sh',
  't5526-fetch-submodules.sh',
  't5527-fetch-odd-refs.sh',
  't5528-push-default.sh',
  't5529-push-errors.sh',
  't5530-upload-pack-error.sh',
  't5531-deep-submodule-push.sh',
  't5532-fetch-proxy.sh',
  't5533-push-cas.sh',
  't5534-push-signed.sh',
  't5535-fetch-push-symref.sh',
  't5536-fetch-conflicts.sh',
  't5537-fetch-shallow.sh',
  't5538-push-shallow.sh',
  't5539-fetch-http-shallow.sh',
  't5540-http-push-webdav.sh',
  't5541-http-push-smart.sh',
  't5542-push-http-shallow.sh',
  't5543-atomic-push.sh',
  't5544-pack-objects-hook.sh',
  't5545-push-options.sh',
  't5546-receive-limits.sh',
  't5547-push-quarantine.sh',
  't5548-push-porcelain.sh',
  't5549-fetch-push-http.sh',
  't5550-http-fetch-dumb.sh',
  't5551-http-fetch-smart.sh',
  't5552-skipping-fetch-negotiator.sh',
  't5553-set-upstream.sh',
  't5554-noop-fetch-negotiator.sh',
  't5555-http-smart-common.sh',
  't5557-http-get.sh',
  't5558-clone-bundle-uri.sh',
  't5559-http-fetch-smart-http2.sh',
  't5560-http-backend-noserver.sh',
  't5561-http-backend.sh',
  't5562-http-backend-content-length.sh',
  't5563-simple-http-auth.sh',
  't5564-http-proxy.sh',
  't5570-git-daemon.sh',
  't5571-pre-push-hook.sh',
  't5572-pull-submodule.sh',
  't5573-pull-verify-signatures.sh',
  't5574-fetch-output.sh',
  't5580-unc-paths.sh',
  't5581-http-curl-verbose.sh',
  't5582-fetch-negative-refspec.sh',
  't5583-push-branches.sh',
  't5600-clone-fail-cleanup.sh',
  't5601-clone.sh',
  't5602-clone-remote-exec.sh',
  't5603-clone-dirname.sh',
  't5604-clone-reference.sh',
  't5605-clone-local.sh',
  't5606-clone-options.sh',
  't5607-clone-bundle.sh',
  't5608-clone-2gb.sh',
  't5609-clone-branch.sh',
  't5610-clone-detached.sh',
  't5611-clone-config.sh',
  't5612-clone-refspec.sh',
  't5613-info-alternate.sh',
  't5614-clone-submodules-shallow.sh',
  't5615-alternate-env.sh',
  't5616-partial-clone.sh',
  't5617-clone-submodules-remote.sh',
  't5618-alternate-refs.sh',
  't5619-clone-local-ambiguous-transport.sh',
  't5620-backfill.sh',
  't5621-clone-revision.sh',
  't5700-protocol-v1.sh',
  't5701-git-serve.sh',
  't5702-protocol-v2.sh',
  't5703-upload-pack-ref-in-want.sh',
  't5704-protocol-violations.sh',
  't5705-session-id-in-capabilities.sh',
  't5710-promisor-remote-capability.sh',
  't5730-protocol-v2-bundle-uri-file.sh',
  't5731-protocol-v2-bundle-uri-git.sh',
  't5732-protocol-v2-bundle-uri-http.sh',
  't5750-bundle-uri-parse.sh',
  't5801-remote-helpers.sh',
  't5802-connect-helper.sh',
  't5810-proto-disable-local.sh',
  't5811-proto-disable-git.sh',
  't5812-proto-disable-http.sh',
  't5813-proto-disable-ssh.sh',
  't5814-proto-disable-ext.sh',
  't5815-submodule-protos.sh',
  't5900-repo-selection.sh',
  't6000-rev-list-misc.sh',
  't6001-rev-list-graft.sh',
  't6002-rev-list-bisect.sh',
  't6003-rev-list-topo-order.sh',
  't6004-rev-list-path-optim.sh',
  't6005-rev-list-count.sh',
  't6006-rev-list-format.sh',
  't6007-rev-list-cherry-pick-file.sh',
  't6008-rev-list-submodule.sh',
  't6009-rev-list-parent.sh',
  't6010-merge-base.sh',
  't6011-rev-list-with-bad-commit.sh',
  't6012-rev-list-simplify.sh',
  't6013-rev-list-reverse-parents.sh',
  't6014-rev-list-all.sh',
  't6016-rev-list-graph-simplify-history.sh',
  't6017-rev-list-stdin.sh',
  't6018-rev-list-glob.sh',
  't6019-rev-list-ancestry-path.sh',
  't6020-bundle-misc.sh',
  't6021-rev-list-exclude-hidden.sh',
  't6022-rev-list-missing.sh',
  't6030-bisect-porcelain.sh',
  't6040-tracking-info.sh',
  't6041-bisect-submodule.sh',
  't6050-replace.sh',
  't6060-merge-index.sh',
  't6100-rev-list-in-order.sh',
  't6101-rev-parse-parents.sh',
  't6102-rev-list-unexpected-objects.sh',
  't6110-rev-list-sparse.sh',
  't6111-rev-list-treesame.sh',
  't6112-rev-list-filters-objects.sh',
  't6113-rev-list-bitmap-filters.sh',
  't6114-keep-packs.sh',
  't6115-rev-list-du.sh',
  't6120-describe.sh',
  't6130-pathspec-noglob.sh',
  't6131-pathspec-icase.sh',
  't6132-pathspec-exclude.sh',
  't6133-pathspec-rev-dwim.sh',
  't6134-pathspec-in-submodule.sh',
  't6135-pathspec-with-attrs.sh',
  't6136-pathspec-in-bare.sh',
  't6137-pathspec-wildcards-literal.sh',
  't6200-fmt-merge-msg.sh',
  't6300-for-each-ref.sh',
  't6301-for-each-ref-errors.sh',
  't6302-for-each-ref-filter.sh',
  't6400-merge-df.sh',
  't6401-merge-criss-cross.sh',
  't6402-merge-rename.sh',
  't6403-merge-file.sh',
  't6404-recursive-merge.sh',
  't6405-merge-symlinks.sh',
  't6406-merge-attr.sh',
  't6407-merge-binary.sh',
  't6408-merge-up-to-date.sh',
  't6409-merge-subtree.sh',
  't6411-merge-filemode.sh',
  't6412-merge-large-rename.sh',
  't6413-merge-crlf.sh',
  't6414-merge-rename-nocruft.sh',
  't6415-merge-dir-to-symlink.sh',
  't6416-recursive-corner-cases.sh',
  't6417-merge-ours-theirs.sh',
  't6418-merge-text-auto.sh',
  't6419-merge-ignorecase.sh',
  't6421-merge-partial-clone.sh',
  't6422-merge-rename-corner-cases.sh',
  't6423-merge-rename-directories.sh',
  't6424-merge-unrelated-index-changes.sh',
  't6425-merge-rename-delete.sh',
  't6426-merge-skip-unneeded-updates.sh',
  't6427-diff3-conflict-markers.sh',
  't6428-merge-conflicts-sparse.sh',
  't6429-merge-sequence-rename-caching.sh',
  't6430-merge-recursive.sh',
  't6431-merge-criscross.sh',
  't6432-merge-recursive-space-options.sh',
  't6433-merge-toplevel.sh',
  't6434-merge-recursive-rename-options.sh',
  't6435-merge-sparse.sh',
  't6436-merge-overwrite.sh',
  't6437-submodule-merge.sh',
  't6438-submodule-directory-file-conflicts.sh',
  't6439-merge-co-error-msgs.sh',
  't6500-gc.sh',
  't6501-freshen-objects.sh',
  't6600-test-reach.sh',
  't6601-path-walk.sh',
  't6700-tree-depth.sh',
  't7001-mv.sh',
  't7002-mv-sparse-checkout.sh',
  't7003-filter-branch.sh',
  't7004-tag.sh',
  't7005-editor.sh',
  't7006-pager.sh',
  't7007-show.sh',
  't7008-filter-branch-null-sha1.sh',
  't7010-setup.sh',
  't7011-skip-worktree-reading.sh',
  't7012-skip-worktree-writing.sh',
  't7030-verify-tag.sh',
  't7031-verify-tag-signed-ssh.sh',
  't7060-wtstatus.sh',
  't7061-wtstatus-ignore.sh',
  't7062-wtstatus-ignorecase.sh',
  't7063-status-untracked-cache.sh',
  't7064-wtstatus-pv2.sh',
  't7101-reset-empty-subdirs.sh',
  't7102-reset.sh',
  't7103-reset-bare.sh',
  't7104-reset-hard.sh',
  't7105-reset-patch.sh',
  't7106-reset-unborn-branch.sh',
  't7107-reset-pathspec-file.sh',
  't7110-reset-merge.sh',
  't7111-reset-table.sh',
  't7112-reset-submodule.sh',
  't7113-post-index-change-hook.sh',
  't7201-co.sh',
  't7300-clean.sh',
  't7301-clean-interactive.sh',
  't7400-submodule-basic.sh',
  't7401-submodule-summary.sh',
  't7402-submodule-rebase.sh',
  't7403-submodule-sync.sh',
  't7406-submodule-update.sh',
  't7407-submodule-foreach.sh',
  't7408-submodule-reference.sh',
  't7409-submodule-detached-work-tree.sh',
  't7411-submodule-config.sh',
  't7412-submodule-absorbgitdirs.sh',
  't7413-submodule-is-active.sh',
  't7414-submodule-mistakes.sh',
  't7416-submodule-dash-url.sh',
  't7417-submodule-path-url.sh',
  't7418-submodule-sparse-gitmodules.sh',
  't7419-submodule-set-branch.sh',
  't7420-submodule-set-url.sh',
  't7421-submodule-summary-add.sh',
  't7422-submodule-output.sh',
  't7423-submodule-symlinks.sh',
  't7424-submodule-mixed-ref-formats.sh',
  't7450-bad-git-dotfiles.sh',
  't7500-commit-template-squash-signoff.sh',
  't7501-commit-basic-functionality.sh',
  't7502-commit-porcelain.sh',
  't7503-pre-commit-and-pre-merge-commit-hooks.sh',
  't7504-commit-msg-hook.sh',
  't7505-prepare-commit-msg-hook.sh',
  't7506-status-submodule.sh',
  't7507-commit-verbose.sh',
  't7508-status.sh',
  't7509-commit-authorship.sh',
  't7510-signed-commit.sh',
  't7511-status-index.sh',
  't7512-status-help.sh',
  't7513-interpret-trailers.sh',
  't7514-commit-patch.sh',
  't7515-status-symlinks.sh',
  't7516-commit-races.sh',
  't7517-per-repo-email.sh',
  't7518-ident-corner-cases.sh',
  't7519-status-fsmonitor.sh',
  't7520-ignored-hook-warning.sh',
  't7521-ignored-mode.sh',
  't7524-commit-summary.sh',
  't7525-status-rename.sh',
  't7526-commit-pathspec-file.sh',
  't7527-builtin-fsmonitor.sh',
  't7528-signed-commit-ssh.sh',
  't7600-merge.sh',
  't7601-merge-pull-config.sh',
  't7602-merge-octopus-many.sh',
  't7603-merge-reduce-heads.sh',
  't7604-merge-custom-message.sh',
  't7605-merge-resolve.sh',
  't7606-merge-custom.sh',
  't7607-merge-state.sh',
  't7608-merge-messages.sh',
  't7609-mergetool--lib.sh',
  't7610-mergetool.sh',
  't7611-merge-abort.sh',
  't7612-merge-verify-signatures.sh',
  't7614-merge-signoff.sh',
  't7615-diff-algo-with-mergy-operations.sh',
  't7700-repack.sh',
  't7701-repack-unpack-unreachable.sh',
  't7702-repack-cyclic-alternate.sh',
  't7703-repack-geometric.sh',
  't7704-repack-cruft.sh',
  't7800-difftool.sh',
  't7810-grep.sh',
  't7811-grep-open.sh',
  't7812-grep-icase-non-ascii.sh',
  't7813-grep-icase-iso.sh',
  't7814-grep-recurse-submodules.sh',
  't7815-grep-binary.sh',
  't7816-grep-binary-pattern.sh',
  't7817-grep-sparse-checkout.sh',
  't7900-maintenance.sh',
  't8001-annotate.sh',
  't8002-blame.sh',
  't8003-blame-corner-cases.sh',
  't8004-blame-with-conflicts.sh',
  't8005-blame-i18n.sh',
  't8006-blame-textconv.sh',
  't8007-cat-file-textconv.sh',
  't8008-blame-formats.sh',
  't8009-blame-vs-topicbranches.sh',
  't8010-cat-file-filters.sh',
  't8011-blame-split-file.sh',
  't8012-blame-colors.sh',
  't8013-blame-ignore-revs.sh',
  't8014-blame-ignore-fuzzy.sh',
  't9001-send-email.sh',
  't9002-column.sh',
  't9003-help-autocorrect.sh',
  't9100-git-svn-basic.sh',
  't9101-git-svn-props.sh',
  't9102-git-svn-deep-rmdir.sh',
  't9103-git-svn-tracked-directory-removed.sh',
  't9104-git-svn-follow-parent.sh',
  't9105-git-svn-commit-diff.sh',
  't9106-git-svn-commit-diff-clobber.sh',
  't9107-git-svn-migrate.sh',
  't9108-git-svn-glob.sh',
  't9109-git-svn-multi-glob.sh',
  't9110-git-svn-use-svm-props.sh',
  't9111-git-svn-use-svnsync-props.sh',
  't9112-git-svn-md5less-file.sh',
  't9113-git-svn-dcommit-new-file.sh',
  't9114-git-svn-dcommit-merge.sh',
  't9115-git-svn-dcommit-funky-renames.sh',
  't9116-git-svn-log.sh',
  't9117-git-svn-init-clone.sh',
  't9118-git-svn-funky-branch-names.sh',
  't9119-git-svn-info.sh',
  't9120-git-svn-clone-with-percent-escapes.sh',
  't9121-git-svn-fetch-renamed-dir.sh',
  't9122-git-svn-author.sh',
  't9123-git-svn-rebuild-with-rewriteroot.sh',
  't9124-git-svn-dcommit-auto-props.sh',
  't9125-git-svn-multi-glob-branch-names.sh',
  't9126-git-svn-follow-deleted-readded-directory.sh',
  't9127-git-svn-partial-rebuild.sh',
  't9128-git-svn-cmd-branch.sh',
  't9129-git-svn-i18n-commitencoding.sh',
  't9130-git-svn-authors-file.sh',
  't9131-git-svn-empty-symlink.sh',
  't9132-git-svn-broken-symlink.sh',
  't9133-git-svn-nested-git-repo.sh',
  't9134-git-svn-ignore-paths.sh',
  't9135-git-svn-moved-branch-empty-file.sh',
  't9136-git-svn-recreated-branch-empty-file.sh',
  't9137-git-svn-dcommit-clobber-series.sh',
  't9138-git-svn-authors-prog.sh',
  't9139-git-svn-non-utf8-commitencoding.sh',
  't9140-git-svn-reset.sh',
  't9141-git-svn-multiple-branches.sh',
  't9142-git-svn-shallow-clone.sh',
  't9143-git-svn-gc.sh',
  't9144-git-svn-old-rev_map.sh',
  't9145-git-svn-master-branch.sh',
  't9146-git-svn-empty-dirs.sh',
  't9147-git-svn-include-paths.sh',
  't9148-git-svn-propset.sh',
  't9150-svk-mergetickets.sh',
  't9151-svn-mergeinfo.sh',
  't9152-svn-empty-dirs-after-gc.sh',
  't9153-git-svn-rewrite-uuid.sh',
  't9154-git-svn-fancy-glob.sh',
  't9155-git-svn-fetch-deleted-tag.sh',
  't9156-git-svn-fetch-deleted-tag-2.sh',
  't9157-git-svn-fetch-merge.sh',
  't9158-git-svn-mergeinfo.sh',
  't9159-git-svn-no-parent-mergeinfo.sh',
  't9160-git-svn-preserve-empty-dirs.sh',
  't9161-git-svn-mergeinfo-push.sh',
  't9162-git-svn-dcommit-interactive.sh',
  't9163-git-svn-reset-clears-caches.sh',
  't9164-git-svn-dcommit-concurrent.sh',
  't9165-git-svn-fetch-merge-branch-of-branch.sh',
  't9166-git-svn-fetch-merge-branch-of-branch2.sh',
  't9167-git-svn-cmd-branch-subproject.sh',
  't9168-git-svn-partially-globbed-names.sh',
  't9169-git-svn-dcommit-crlf.sh',
  't9200-git-cvsexportcommit.sh',
  't9210-scalar.sh',
  't9211-scalar-clone.sh',
  't9300-fast-import.sh',
  't9301-fast-import-notes.sh',
  't9302-fast-import-unpack-limit.sh',
  't9303-fast-import-compression.sh',
  't9304-fast-import-marks.sh',
  't9350-fast-export.sh',
  't9351-fast-export-anonymize.sh',
  't9400-git-cvsserver-server.sh',
  't9401-git-cvsserver-crlf.sh',
  't9402-git-cvsserver-refs.sh',
  't9500-gitweb-standalone-no-errors.sh',
  't9501-gitweb-standalone-http-status.sh',
  't9502-gitweb-standalone-parse-output.sh',
  't9600-cvsimport.sh',
  't9601-cvsimport-vendor-branch.sh',
  't9602-cvsimport-branches-tags.sh',
  't9603-cvsimport-patchsets.sh',
  't9604-cvsimport-timestamps.sh',
  't9700-perl-git.sh',
  't9800-git-p4-basic.sh',
  't9801-git-p4-branch.sh',
  't9802-git-p4-filetype.sh',
  't9803-git-p4-shell-metachars.sh',
  't9804-git-p4-label.sh',
  't9805-git-p4-skip-submit-edit.sh',
  't9806-git-p4-options.sh',
  't9807-git-p4-submit.sh',
  't9808-git-p4-chdir.sh',
  't9809-git-p4-client-view.sh',
  't9810-git-p4-rcs.sh',
  't9811-git-p4-label-import.sh',
  't9812-git-p4-wildcards.sh',
  't9813-git-p4-preserve-users.sh',
  't9814-git-p4-rename.sh',
  't9815-git-p4-submit-fail.sh',
  't9816-git-p4-locked.sh',
  't9817-git-p4-exclude.sh',
  't9818-git-p4-block.sh',
  't9819-git-p4-case-folding.sh',
  't9820-git-p4-editor-handling.sh',
  't9821-git-p4-path-variations.sh',
  't9822-git-p4-path-encoding.sh',
  't9823-git-p4-mock-lfs.sh',
  't9824-git-p4-git-lfs.sh',
  't9825-git-p4-handle-utf16-without-bom.sh',
  't9826-git-p4-keep-empty-commits.sh',
  't9827-git-p4-change-filetype.sh',
  't9828-git-p4-map-user.sh',
  't9829-git-p4-jobs.sh',
  't9830-git-p4-symlink-dir.sh',
  't9831-git-p4-triggers.sh',
  't9832-unshelve.sh',
  't9833-errors.sh',
  't9834-git-p4-file-dir-bug.sh',
  't9835-git-p4-metadata-encoding-python2.sh',
  't9836-git-p4-metadata-encoding-python3.sh',
  't9850-shell.sh',
  't9901-git-web--browse.sh',
  't9902-completion.sh',
  't9903-bash-prompt.sh',
]

benchmarks = [
  'perf/p0000-perf-lib-sanity.sh',
  'perf/p0001-rev-list.sh',
  'perf/p0002-read-cache.sh',
  'perf/p0003-delta-base-cache.sh',
  'perf/p0004-lazy-init-name-hash.sh',
  'perf/p0005-status.sh',
  'perf/p0006-read-tree-checkout.sh',
  'perf/p0007-write-cache.sh',
  'perf/p0008-odb-fsync.sh',
  'perf/p0071-sort.sh',
  'perf/p0090-cache-tree.sh',
  'perf/p0100-globbing.sh',
  'perf/p1006-cat-file.sh',
  'perf/p1400-update-ref.sh',
  'perf/p1450-fsck.sh',
  'perf/p1451-fsck-skip-list.sh',
  'perf/p1500-graph-walks.sh',
  'perf/p1501-rev-parse-oneline.sh',
  'perf/p2000-sparse-operations.sh',
  'perf/p3400-rebase.sh',
  'perf/p3404-rebase-interactive.sh',
  'perf/p4000-diff-algorithms.sh',
  'perf/p4001-diff-no-index.sh',
  'perf/p4002-diff-color-moved.sh',
  'perf/p4205-log-pretty-formats.sh',
  'perf/p4209-pickaxe.sh',
  'perf/p4211-line-log.sh',
  'perf/p4220-log-grep-engines.sh',
  'perf/p4221-log-grep-engines-fixed.sh',
  'perf/p5302-pack-index.sh',
  'perf/p5303-many-packs.sh',
  'perf/p5304-prune.sh',
  'perf/p5310-pack-bitmaps.sh',
  'perf/p5311-pack-bitmaps-fetch.sh',
  'perf/p5312-pack-bitmaps-revs.sh',
  'perf/p5313-pack-objects.sh',
  'perf/p5314-name-hash.sh',
  'perf/p5326-multi-pack-bitmaps.sh',
  'perf/p5332-multi-pack-reuse.sh',
  'perf/p5333-pseudo-merge-bitmaps.sh',
  'perf/p5550-fetch-tags.sh',
  'perf/p5551-fetch-rescan.sh',
  'perf/p5600-partial-clone.sh',
  'perf/p5601-clone-reference.sh',
  'perf/p6100-describe.sh',
  'perf/p6300-for-each-ref.sh',
  'perf/p7000-filter-branch.sh',
  'perf/p7102-reset.sh',
  'perf/p7300-clean.sh',
  'perf/p7519-fsmonitor.sh',
  'perf/p7527-builtin-fsmonitor.sh',
  'perf/p7810-grep.sh',
  'perf/p7820-grep-engines.sh',
  'perf/p7821-grep-engines-fixed.sh',
  'perf/p7822-grep-perl-character.sh',
  'perf/p9210-scalar.sh',
  'perf/p9300-fast-import-export.sh',
]

# Sanity check that we are not missing any tests present in 't/'. This check
# only runs once at configure time and is thus best-effort, only. It is
# sufficient to catch missing test suites in our CI though.
foreach glob, tests : {
  't[0-9][0-9][0-9][0-9]-*.sh': integration_tests,
  'perf/p[0-9][0-9][0-9][0-9]-*.sh': benchmarks,
  'unit-tests/t-*.c': unit_test_programs,
  'unit-tests/u-*.c': clar_test_suites,
}
  actual_tests = run_command(shell, '-c', 'ls ' + glob,
    check: true,
    env: script_environment,
  ).stdout().strip().split('\n')

  if tests != actual_tests
    missing_tests = [ ]
    foreach actual_test : actual_tests
      if actual_test not in tests
        missing_tests += actual_test
      endif
    endforeach
    if missing_tests.length() > 0
      error('Test files found, but not configured:\n\n - ' + '\n - '.join(missing_tests))
    endif

    superfluous_tests = [ ]
    foreach integration_test : tests
      if integration_test not in actual_tests
        superfluous_tests += integration_test
      endif
    endforeach
    if superfluous_tests.length() > 0
      error('Test files configured, but not found:\n\n - ' + '\n - '.join(superfluous_tests))
    endif
  endif
endforeach

# GIT_BUILD_DIR needs to be Unix-style without drive prefixes as it get added
# to the PATH variable. And given that drive prefixes contain a colon we'd
# otherwise end up with a broken PATH if we didn't convert it.
git_build_dir = meson.project_build_root()
if cygpath.found()
  git_build_dir = run_command(cygpath, git_build_dir, check: true).stdout().strip()
endif

test_environment = script_environment
test_environment.set('GIT_BUILD_DIR', git_build_dir)

foreach integration_test : integration_tests
  test(fs.stem(integration_test), shell,
    args: [ integration_test ],
    workdir: meson.current_source_dir(),
    env: test_environment,
    depends: test_dependencies + bin_wrappers,
    kwargs: test_kwargs,
  )
endforeach

if perl.found() and time.found()
  benchmark_environment = test_environment
  benchmark_environment.set('GTIME', time.full_path())

  foreach benchmark : benchmarks
    benchmark(fs.stem(benchmark), shell,
      args: [
        fs.name(benchmark),
      ],
      workdir: meson.current_source_dir() / 'perf',
      env: benchmark_environment,
      depends: test_dependencies + bin_wrappers,
      timeout: 0,
    )
  endforeach
endif
