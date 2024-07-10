# MyGNUHealth Flatpak

This is the [MyGNUHealth](https://docs.gnuhealth.org/mygnuhealth/) Flatpak.


# Users

This section covers installation instructions and additional information for MyGNUHealth users.

### Install

Add the Flathub remote.

    flatpak --user remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

Install the MyGNUHealth Flatpak.

    flatpak --user install -y flathub org.gnuhealth.mygnuhealth

### Known issues

#### Fonts and user elements are too big or too small.

This is an upstream scaling issue.
Read the `Manual control of metrics` section in the [Kivy documentation](https://kivy.org/doc/stable/_modules/kivy/metrics.html)
and try to find the right `KIVY_DPI`, `KIVY_METRICS_DENSITY` (and optinally the `KIVY_METRICS_FONTSCALE`) value for your screen.
For example:

```bash
flatpak run --devel --command=bash org.gnuhealth.mygnuhealth
`KIVY_DPI=320 KIVY_METRICS_DENSITY=2.0 mygnuhealth --size 720x1440`
```

Once you have the right values you can set them permanenty on this package:

```bash
flatpak override --env="KIVY_DPI=320 KIVY_METRICS_DENSITY=2.0" org.gnuhealth.mygnuhealth
```

## Maintainers

### Build

Get the build dependencies.

    flatpak --user install -y flathub org.freedesktop.Platform//23.08 org.freedesktop.Sdk//23.08

Get the source code.

    git clone https://github.com/flathub/org.gnuhealth.mygnuhealth
    cd org.gnuhealth.mygnuhealth

Add the Flathub repository.

    flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

Install Flatpak Builder.

    sudo apt install flatpak-builder

Build the Flatpak.

    flatpak-builder --user --install --install-deps-from=flathub --force-clean --repo=repo build-dir org.gnuhealth.mygnuhealth.yaml

Run the Flatpak.

    flatpak run org.gnuhealth.MyGNUHealth
