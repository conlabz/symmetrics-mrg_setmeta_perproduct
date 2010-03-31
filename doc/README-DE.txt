* DOCUMENTATION

** INSTALLATION
Extrahieren Sie den Inhalt dieses Archivs in Ihr Magento Verzeichnis.
! Das Attribut 'generate_meta' muss dem/einem Attributset hinzugef�gt werden. !

** USAGE
Dieses Modul f�llt die Meta-Daten eines Produktes automatisch mit dem Produktnamen und den Kategorien.

** FUNCTIONALITY
*** A: F�gt ein Produktattribut "Generate Meta Data" hinzu
*** B: Wenn dieses Drop-Down auf Ja steht, greift der observer und f�llt den Metatitel mit dem Produktnamen
        und die Beschreibung und Keywords mit einer Komma-Seperierten Liste aus Produktnamen und Kategorienamen.
*** C: Auch wenn diese Drop-Down bei einer Massenbearbeitung auf ja gesetzt wird, werden die Metadaten ausgef�llt.
*** D: Auch Multistore Umgebungen werden ber�cksichtigt. Die Kategorie- und produktnamen werden dann entsprechend
        dem store view eingetragen.

** TECHNINCAL
Via Migrationsskript wird ein Produktattribut 'generate_meta' eingef�gt. Es ist ein Ja/Nein Drop-Down.
Es wird das Event 'catalog_product_save_after' abgefangen, welches bei einer einfachen Produktspeicherung
ausgel�st wird. Hier wird gepr�ft, ob das Produktattribut 'generate_meta' auf "Ja" steht. Tut es das, 
werden die Meta Felder entsprechend gef�llt.
F�r Mass Actions wird das Event 'controller_action_postdispatch_adminhtml_catalog_product_action_attribute_save'
abgefangen. Aus der Session werden dann die produkt IDs geholt und gepr�ft, ob das 'generate_meta' Drop-Down auf "Ja"
gestellt wurde. Dann wird f�r jede ID das Produkt-Model geladen und die Werte gef�llt und gespeichert.

** PROBLEMS

* TESTCASES

** BASIC
*** 0: Pr�fen Sie, ob das vom Migrationsskript angelegte Attribut 'generate_meta' im Attributset vorhanden ist.
        Es sollte dann auftauchen, wenn man das Produkt bearbeitet.
*** A: Pr�fen Sie, ob in der Attributverwaltung das Attribut 'generate_meta' auftaucht.
*** B:	1. Legen Sie im Backend �ber Catalog->Add Product ein neues Produkt an.
	    2. Geben Sie wenigstens die ben�tigten Attribute und eine Kategorie an
	    3. Das Feld "Generate Meta Data" sollte auf "Ja" stehen
	    4. W�hlen Sie "Save & Continue Edit".
	    5. Die Meta-Felder sollten nun mir den Kategorie und Namensinformationen gef�llt werden.
	    6. �ndern Sie den produkt namen und/oder die kategorien und stellen das Drop-Down erneut auf "ja"
	    7. Die Meta Daten sollten sich entsprechend aktualisieren.
	    8. Wiederholen Sie die Schritte 1-5, w�hlen Sie bei Schritt 3 aber "nein" aus.
	    9. Bearbeiten Sie das zuletzt angelegte Produkt und stellen das Drop-Down auf "ja".
	   10. Nach dem Speichern sollten die Meta Daten ausgef�llt worden sein.
*** C:  1. Wiederholen Sie die Schritte 1-5 mehrfach, w�hlen Sie bei Schritt 3 aber "nein" aus.
        2. Machen Sie eine Massen-Bearbeitung der Produkte und stellen das Drop-Down auf "ja".
        3. Pr�fen Sie die Produkte einzeln, sie sollten jetzt alle die entsprechenden Meta Daten haben.
*** D:  1. Wiederholen Sie die Testcases B+C aber w�hlen einen store-scope aus.
	    
** STRESS
Die Produkte m�ssen bei einer Mass Action alle einzeln geladen werde. Dies kann sich negativ auf die Performance auswirken.
Wenn das Drop-Down "Generate Meta Data" nicht auf "ja" steht, werden die Produkte aber nicht einzeln geladen.