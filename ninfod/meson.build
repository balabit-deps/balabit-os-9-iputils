# Copyright (c) Iputils Project, 2017-2020

inc = include_directories('..')
ninfod_sources = files('''
	icmp6_nodeinfo.h
	ni_ifaddrs.c
	ni_ifaddrs.h
	ninfod.c
	ninfod.h
	ninfod_addrs.c
	ninfod_core.c
	ninfod_name.c
'''.split())
ninfod = executable('ninfod', [ninfod_sources, git_version_h],
	dependencies : [cap_dep, rt_dep, threads],
	link_with : [libcommon],
	include_directories : inc,
	install: true,
	install_dir: sbindir)
conf_data = configuration_data()
conf_data.set('prefix', prefix)

if install_systemd_units
	subs = configuration_data()
	subs.set('sbindir', sbindir)
	unit_file = configure_file(
		input: '../systemd/ninfod.service.in',
		output: 'ninfod.service',
		configuration: subs
	)
	install_data(unit_file, install_dir: systemdunitdir)
else
	configure_file(input : 'ninfod.sh.in',
		output : 'ninfod.sh',
		configuration : conf_data,
		install_dir : join_paths(get_option('sysconfdir'), 'init.d'))
endif
