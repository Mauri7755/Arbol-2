# Arbol-2
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Segundo_Arbol
{
    class Arbol2
    {
        public class Nodo
        {
            private int dato;
            private Nodo izquierdo, derecho;

            public Nodo(int dato, Nodo izq, Nodo der)
            {
                this.dato = dato;
                this.izquierdo = izq;
                this.derecho = der;
            }

            public virtual int Dato
            {
                get
                {
                    return dato;
                }
                set
                {
                    this.dato = value;
                }
            }

            //Ramas izquierdas
            public virtual Nodo izquierdo1
            {
                get
                {
                    return izquierdo;
                }
                set
                {
                    this.izquierdo = value;
                }
            }

            //Ramas derechas
            public virtual Nodo Derecho1
            {
                get
                {
                    return derecho;
                }
                set
                {
                    this.derecho = value;
                }
            }


        }

        public class ArbolBinary
        {

            private Nodo root;
            internal int cant;
            internal int Altura;

            public ArbolBinary()
            {
                this.root = null;
            }
            //Metods que agregan los datos
            public virtual void Agregar(int dato)
            {
                Nodo nuevo = new Nodo(dato, null, null);
                Insert(nuevo, root);
            }

            public virtual void Insert(Nodo nuevo, Nodo pivote)
            {
                if (this.root == null)
                {
                    root = nuevo;
                }
                else
                {
                    if (nuevo.Dato <= pivote.Dato)
                    {
                        if (pivote.izquierdo1 == null)
                        {
                            pivote.izquierdo1 = nuevo;
                        }
                        else
                        {
                            Insert(nuevo, pivote.izquierdo1);
                        }
                    }
                    else
                    {
                        if (pivote.Derecho1 == null)
                        {
                            pivote.Derecho1 = nuevo;
                        }
                        else
                        {
                            Insert(nuevo, pivote.Derecho1);
                        }
                    }
                }

            }
            //Nodos
            public virtual bool Exist(int info)
            {
                Nodo reco = root;
                while (reco != null)
                {
                    if (info == reco.Dato)
                    {
                        return true;
                    }
                    else if (info > reco.Dato)
                    {
                        reco = reco.Derecho1;
                    }
                    else
                    {
                        reco = reco.izquierdo1;
                    }
                }
                return false;
            }

            public virtual int Cantidad()
            {
                cant = 0;
                Cantidad(root);
                return cant;
            }
            //Metodos de hojas
            private void Cantidad(Nodo reco)
            {
                if (reco != null)
                {
                    cant++;
                    Cantidad(reco.izquierdo1);
                    Cantidad(reco.Derecho1);
                }
            }

            private void CantidadNodosLeaf(Nodo reco)
            {
                if (reco != null)
                {
                    if (reco.izquierdo1 == null && reco.Derecho1 == null)
                    {
                        cant++;
                    }
                    CantidadNodosLeaf(reco.izquierdo1);
                    CantidadNodosLeaf(reco.Derecho1);
                }
            }

            public virtual int CantidadNodosLeaf()
            {
                cant = 0;
                CantidadNodosLeaf(root);
                return cant;
            }
            //Metodos de como obtener la Altura
            public virtual int ReturnAltura()
            {
                Altura = 0;
                ReturnAltura(root, 1);
                return Altura;
            }
            private void ReturnAltura(Nodo reco, int nivel)
            {
                if (reco != null)
                {
                    ReturnAltura(reco.izquierdo1, nivel + 1);
                    if (nivel > Altura)
                    {
                        Altura = nivel;
                    }
                    ReturnAltura(reco.Derecho1, nivel + 1);
                }
            }
            //Altura arbol
            internal string[] niveles;

            public virtual int AlturaArbol()
            {
                Altura = 0;
                AlturaArbol(root, 0);
                return Altura;
            }
            private void AlturaArbol(Nodo pivote, int nivel)
            {
                if (pivote != null)
                {
                    AlturaArbol(pivote.izquierdo1, nivel + 1);
                    if (nivel > Altura)
                    {
                        Altura = nivel;
                    }
                    AlturaArbol(pivote.Derecho1, nivel + 1);
                }
            }
            //Metodos del nivel
            public virtual void Printnivel()
            {
                niveles = new string[Altura + 1];

                Printnivel(root, 0);
                for (int i = 0; i < niveles.Length; i++)
                {
                    Console.WriteLine(niveles[i] + " En nivel: " + i);
                }
            }
            public virtual void Printnivel(Nodo pivote, int lvl)
            {
                if (pivote != null)
                {
                    niveles[lvl] = pivote.Dato + ", " + ((!string.ReferenceEquals(niveles[lvl], null)) ? niveles[lvl] : "");
                    Printnivel(pivote.Derecho1, lvl + 1);
                    Printnivel(pivote.izquierdo1, lvl + 1);
                }
            }
            public virtual void PrintAlturaDeCadaNod()
            {
                PrintAlturaDeCadaNod(root, 1);
            }
            private void PrintAlturaDeCadaNod(Nodo reco, int nivel)
            {
                if (reco != null)
                {
                    Console.WriteLine("Nodo contiene: " + reco.Dato + " y su Altura es: " + nivel);
                    PrintAlturaDeCadaNod(reco.izquierdo1, nivel + 1);
                    PrintAlturaDeCadaNod(reco.Derecho1, nivel + 1);
                }
            }
        }

        static void Main(string[] args)
        {
            ArbolBinary raiz = new ArbolBinary();
            int ob;
            int a = 2, b = 72, c = 6, d = 62, e = 54, f = 53, g=56,h=58,i=64,j=69,k=52;
            Console.WriteLine(" Insertando valores manualmente en el árbol: ");
            raiz.Agregar(a);
            raiz.Agregar(b);
            raiz.Agregar(c);
            raiz.Agregar(d);
            raiz.Agregar(e);
            raiz.Agregar(f);
            raiz.Agregar(g);
            raiz.Agregar(h);
            raiz.Agregar(i);
            raiz.Agregar(j);
            raiz.Agregar(k);

            Console.WriteLine(" "+" "+" "+" "+" "+" "+"/"+"j");
            Console.WriteLine("/"+"b"+" "+" "+"/"+"i"+" "+" "+"/"+"h");
            Console.WriteLine("|--"+"d"+" "+" "+" "+"/"+"g");
            Console.WriteLine("k"+" "+" "+"|_"+"e");
            Console.WriteLine("|_"+"c"+" "+" "+" "+"|_"+"f");
            Console.WriteLine("|_"+"a");

            Console.WriteLine("Valores insertados: " + a + " " + b + " " + c + " " + d + " " + e + " " + f + " ");
            raiz.PrintAlturaDeCadaNod();
            do
            {
                Console.WriteLine(" ");
                Console.WriteLine(" ");
                Console.WriteLine("1.-Cantidad de nodos del arbol.");
                Console.WriteLine("2.-Cantidad de nodos hoja.");
                Console.WriteLine("3.-Altura del arbol.");
                Console.WriteLine("0.-Salir");
                ob = int.Parse(Console.ReadLine());
                switch (ob)
                {
                    case 1:
                        Console.WriteLine("Cantidad de nodos del árbol:" + raiz.Cantidad());
                        break;
                    case 2:
                        Console.WriteLine("Cantidad de nodos hoja:" + raiz.CantidadNodosLeaf());
                        break;
                    case 3:
                        Console.WriteLine("La Altura del arbol es:" + raiz.ReturnAltura());
                        break;
                }
            } while (ob != 0);
            Console.ReadKey();
        } 
    } 
}

