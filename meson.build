project('simplewgconfig',
          version: '0.1.0',
    meson_version: '>= 1.0.0',
  default_options: [ 'warning_level=2', 'werror=false', ],
)


install_data('simplewgconfig', install_dir: get_option('bindir'),install_mode: 'r-xr-xr-x')


application_id = 'com.github.yucefsourani.simplewgconfig'

scalable_dir = join_paths('hicolor', 'scalable', 'apps')
install_data(
  join_paths(('@0@.svg').format(application_id)),
  install_dir: join_paths(get_option('datadir'), 'icons', scalable_dir)
)

symbolic_dir = join_paths('hicolor', 'symbolic', 'apps')
install_data(
  join_paths(('@0@-symbolic.svg').format(application_id)),
  install_dir: join_paths(get_option('datadir'), 'icons', symbolic_dir)
)


install_data(
  join_paths('hicolor/512x512/apps', ('@0@.png').format(application_id)),
  install_dir: join_paths(get_option('datadir'), 'pixmaps')
)

allsize = ['8', '16', '22', '24', '32', '36', '42', '64', '72', '96', '128', '256', '512']
foreach size : allsize
    icon_dir = join_paths('hicolor', ('@0@x@1@').format(size,size), 'apps')
    install_data(
      join_paths(icon_dir, ('@0@.png').format(application_id)),
        install_dir: join_paths(get_option('datadir'), 'icons', icon_dir)
     )
endforeach



desktop_file = ('@0@.desktop').format(application_id)
install_data(
  desktop_file,
  install_dir: get_option('datadir') / 'applications'
)

desktop_utils = find_program('desktop-file-validate', required: false)
if desktop_utils.found()
  test('Validate desktop file', desktop_utils, args: [desktop_file])
endif


appstream_file = ('@0@.metainfo.xml').format(application_id)
install_data(
  appstream_file,
  install_dir: get_option('datadir') / 'metainfo'
)

appstreamcli = find_program('appstreamcli', required: false, disabler: true)
test('Validate appstream file', appstreamcli,
     args: ['validate', '--no-net', '--explain', appstream_file])