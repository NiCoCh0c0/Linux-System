In most Linux systems, system will give an id to the machine. This id isn't specific to hardware or network. It defines a system, a particular machine whatever if a configuration change.
The id is a single newline-terminated, hexadecimal, 32 caracter, lowercase ID stored in /etc/machine-id.
On some system, it also can be stored in /etc/lib/dbus/machine-id.
Usally, it's define randomly on the first boot. In fact, with the presence or abscence of this machine-id, the system will know if it's a first boot.
On the first boot, systemd will write "uninitialized\n" until the end of the installation sequence. Like that, systemd can understand if it was a problem during the installation.
If the file contained "unilitialized" at the start, the system will consired it's a first boot.
If the file exist but it's empty, the system understand that's not the first boot ! The system will write a new id. It's particulary usefull when you are duplicating a system. Maybe you're using VM's or container's and don't
want the system to act like a first boot (you probably made a template with some services installed and configured), you can still generate a new one without taking the risk of an id duplication.
Please, note that is id is considered secret.

If you want to recreate a machine id :
```bash
rm -f /etc/machine-id /var/lib/dbus/machine-id
dbus-uuidgen --ensure=/etc/machine-id
dbus-uuidgen --ensure
```
If you want to empty the machine-id file :
```bash
sudo truncate -s 0 /etc/machine-id
```
