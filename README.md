# Miniflux LazyCat community package

Source https://github.com/miniflux/v2,2.3.4,Apache-2.0. Official candidate wcloud.gblw.app.miniflux. Package community.lazycat.app.miniflux,minOS1.5.0,amd64 mirror delivery, community store only. Intended category News/RSS49.

Two containers: Miniflux HTTP8080 and internal PostgreSQL18-alpine. Persist the whole PostgreSQL18 parent directory at /lzcapp/var/postgres:/var/lib/postgresql; do not change database major in place. Keep backups before uninstalling. Database port is not exposed. The pg_isready healthcheck is copied from upstream, no new smoke job.

Use native RUN_MIGRATIONS and CREATE_ADMIN bootstrap. Shared initial admin uses a deployment secret, /login #form-username and native credential field autofill without auto-submit, platform auth retained. Existing database users are not reset by changing deployment params; keep them synchronized after changing credentials inside Miniflux. All granted members can use the shared admin fill; only authorize trusted people. Native extra users/API clients need their own account/entry authentication design.

The database credential is derived as hex of a stable secret via the native Go printf function, avoiding URI-reserved characters; the identical expression supplies PostgreSQL and the application URI. No external credential is embedded.

Build and independent package SHA256/config checks run on GitHub, no local source/image/LPK downloads. No file interception or new smoke checks. Startup, migrations, initial account, autofill, feed fetching and restart persistence have not been runtime-verified.
