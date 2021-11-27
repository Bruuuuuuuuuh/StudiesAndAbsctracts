Enums are a type of data structure equal to each other and arranged, with no classes 
like String, int, boolean, or double to specify their type.

You can say that they are non-specified-class's Arrays.

All enum tipes implicitly extend the java.lang.Enum class, and don't suport multiple 
heritage.

Some caracteristics about enums:

    Instances of enum types are created and named along with the class declaration, 
    being fixed and immutable (the value is fixed).;

    It is not allowed to create new instances with the new keyword;

    The constructor is declared private, although it doesn't need an explicit private modifier;

    Following the convention, as they are constant and immutable objects (static final),
    the declared names receive all letters in UPPERCASE;

    Instances of enum types must have only one name;

    Optionally, the class declaration can include instance variables, constructor, instance
    methods, class, etc.
      
      
Examples of enums:

    package com.pernalonga.helpdesk.domain.enums;

    public enum Perfil {
	
      ADMIN(0, "ROLE_ADMIN"), CLIENT(1, "ROLE_CLIENT"), TECNIC(2, "ROLE_TECNIC");

      private Integer codigo;
      private String descricao;

      private Perfil(Integer codigo, String descricao) {
        this.codigo = codigo;
        this.descricao = descricao;
      }

      public Integer getCodigo() {
        return codigo;
      }

      public String getDescricao() {
        return descricao;
      }

      public static Perfil toEnum(Integer cod) {
        if(cod == null) {
          return null;
        }

        for(Perfil x : Perfil.values()) {
          if(cod.equals(x.getCodigo())) {
            return x;
          }
        }

        throw new IllegalArgumentException("Perfil invalido");
      }

    }

      
