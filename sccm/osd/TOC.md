# Verstehen und Kennenlernen
## [Einführung in die Betriebssystembereitstellung](understand/introduction-to-operating-system-deployment.md)
## [Tasksequenzschritte](understand/task-sequence-steps.md)
## [Tasksequenz-Aktionsvariablen](understand/task-sequence-action-variables.md)
## [Integrierte Tasksequenzvariablen](understand/task-sequence-built-in-variables.md)
## [Prestart-Befehle für Tasksequenzmedien](understand/prestart-commands-for-task-sequence-media.md)

# Planung und Entwurf
## [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](plan-design/infrastructure-requirements-for-operating-system-deployment.md)
## [Planungsüberlegungen für das Automatisieren von Tasks](plan-design/planning-considerations-for-automating-tasks.md)
## [Sicherheit und Datenschutz für die Betriebssystembereitstellung](plan-design/security-and-privacy-for-operating-system-deployment.md)
## [Planen der Interoperabilität der Betriebssystembereitstellung](plan-design/planning-for-operating-system-deployment-interoperability.md)

# Erste Schritte
## [Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen](get-started/prepare-site-system-roles-for-operating-system-deployments.md)
## [Vorbereiten auf die Betriebssystembereitstellung](get-started/prepare-for-operating-system-deployment.md)
### [Verwalten von Startimages](get-started/manage-boot-images.md)
#### [Anpassen von Startimages](get-started/customize-boot-images.md)

### [Verwalten von Betriebssystemimages](get-started/manage-operating-system-images.md)
#### [Anpassen von Betriebssystemimages](get-started/customize-operating-system-images.md)

### [Verwalten von Betriebssystem-Upgradepaketen](get-started/manage-operating-system-upgrade-packages.md)
### [Verwalten von Treibern](get-started/manage-drivers.md)
### [Verwalten des Benutzerzustands](get-started/manage-user-state.md)
### [Vorbereiten auf Bereitstellungen für unbekannte Computer](get-started/prepare-for-unknown-computer-deployments.md)
### [Zuordnen von Benutzern zu einem Zielcomputer](get-started/associate-users-with-a-destination-computer.md)

## [Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs](get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)

# Bereitstellen und Verwenden
## [Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)
### [Upgrade von Windows auf die neueste Version](deploy-use/upgrade-windows-to-the-latest-version.md)
### [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)
### [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](deploy-use/install-new-windows-version-new-computer-bare-metal.md)
### [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](deploy-use/replace-an-existing-computer-and-transfer-settings.md)

## [Methoden zum Bereitstellen von Unternehmensbetriebssystemen](deploy-use/methods-to-deploy-enterprise-operating-systems.md)
### [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](deploy-use/use-pxe-to-deploy-windows-over-the-network.md)
### [Use Software Center to deploy Windows over the network (Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk)](deploy-use/use-software-center-to-deploy-windows-over-the-network.md)
### [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md)
### [Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks](deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
### [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](deploy-use/use-multicast-to-deploy-windows-over-the-network.md)
### [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
### [Bereitstellen von Windows To Go](deploy-use/deploy-windows-to-go.md)

## [Verwalten von Windows as a Service](deploy-use/manage-windows-as-a-service.md)
## [Überwachen von Betriebssystembereitstellungen](deploy-use/monitor-operating-system-deployments.md)

## [Verwalten von Tasksequenzen zum Automatisieren von Tasks](deploy-use/manage-task-sequences-to-automate-tasks.md)
### [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](deploy-use/create-a-task-sequence-to-install-an-operating-system.md)
### [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
### [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)
### [Erstellen einer Tasksequenz zum Erfassen und Wiederherstellen des Benutzerstatus](deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)
### [Verwenden einer Tasksequenz zum Verwalten virtueller Festplatten](deploy-use/use-a-task-sequence-to-manage-virtual-hard-disks.md)

## [Benutzerdefinierte Tasksequenzszenarios](deploy-use/custom-task-sequence-scenarios.md)
### [Erstellen einer benutzerdefinierten Tasksequenz](deploy-use/create-a-custom-task-sequence.md)
### [Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen](deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)
### [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)

## [Erstellen von Tasksequenzmedien](deploy-use/create-task-sequence-media.md)
### [Erstellen eigenständiger Medien](deploy-use/create-stand-alone-media.md)
### [Erstellen von vorab bereitgestellten Medien](deploy-use/create-prestaged-media.md)
### [Erstellen von startbaren Medien](deploy-use/create-bootable-media.md)
### [Erstellen von Erfassungsmedien](deploy-use/create-capture-media.md)


<!--HONumber=Dec16_HO3-->


