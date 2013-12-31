SSiED
=====

Tworzenie operator�w - tutorial
--------------------------------------------
W folderze <a href="https://github.com/elkorn/SSiED/tree/master/project">project</a> znajduj� si� projekty dla eclipse:

* RapidMiner\_Extension\_Template_Unuk
* Rapidminer_Unuk

Do skompilowania rozszerzenia dla rapidminera potrzebne s� obydwa projekty.

Nowe operatory definiowane s� w projekcie ``RapidMiner_Extension_Template_Unuk``. Przepis jak to zrobi�:

1.  W katalogu ``src/com/rapidminer/`` definiujemy now� klas� dla operatora.

2.  Nowa klasa powinna rozszerza� klas� ``Operator`` i nadpisa� nast�puj�ce metody:

 ``doWork`` - funkcje realizowane w trakcie przetwarzania danych

 ``getParameterTypes`` - parametry operatora

 Wej�cia i wyj�cia operatora definiowane s� jako pola klasy:

        private final InputPort exampleSetInput = getInputPorts().createPort("nazwa wejscia");
        private final OutputPort exampleSetOutput = getOutputPorts().createPort("nazwa wyjscia");

 Konstruktor ma posta�:

        public NowyOperator(OperatorDescription description){
	          super(description);
        }

 W ciele konstruktora typowe jest nadawanie warunk�w pocz�tkowych dla wej��/wyj��, ale tylko jak chcemy mie� warninga w rapidminerze gdy co� nie jest pod��czone.

 Przyk�adowe odbieranie danych z port�w/ wysy�anie na port:

        ExampleSet inputExampleSet = exampleSetInput.getData(ExampleSet.class);
        exampleSetOutput.deliver(result); 

 Mo�na si� posi�kowa� istniej�cym operatorem.
3.  Po zdefiniowaniu klasy nale�y przej�� do katalogu ``resources/com/rapidminer/resources/`` i w pliku ``BalancingOperators.xml`` doda� informacje o swoim operatorze:

        <group key="">
          <group key="data_transformation">
	        <group key="data_balancing">
	          <operator>
	            <key>unikalna_nazwa</key>
	            <class>com.rapidminer.NowyOperator</class>
	          </operator>
	        </group>
          </group>
        </group>

 Znaczniki ``<group key="nazwa">`` informuj� w jakiej kategorii zostanie umieszczony nowy operator (panel ``Operators`` w rapidminerze).

4.  Nazwa nadana w tagach ``<key></key>`` mo�e zosta� u�yta do t�umaczenia nazwy operatora w pliku ``OperatorsDocTemplate.xml`` w katalogu``resources/com/rapidminer/resources/i18n/``. 


        <operator>
		  <key>unikalny_nazwa</key>
		    <name>Nazwa widoczna w rapidmierze</name>
		    <synopsis>Kr�tki opis</synopsis>
		    <help>D�ugi opis</help>
	    </operator>


5.  Budujemy projekt Ant'em poprzez plik ``build.xml``  (PPM -> Run as -> Ant build) w g��wnym katalogu.


 Zbudowane rozszerzenie znajdzie si� w projekcie ``Rapidminer_Unuk`` w folderze ``lib/plugins``. Wystarczy uruchomi� ``lib/rapidminer.jar`` i wszystko powinno dzia�a�. Rozszerzenie mo�na te� skopiowa� do analogicznego folderu w rapidminerze 6 i te� zadzia�a.
