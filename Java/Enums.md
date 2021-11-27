Enums are a type of data structure equal to each other and arranged, with no classes 
like String, int, boolean, or double to specify their type.

You can say that they are non-specified-class's Arrays.

All enum tipes implicitly extend the java.lang.Enum class, and don't suport multiple 
heritage.

Some caracteristics about enums:

    . Instances of enum types are created and named along with the class declaration, 
    
    being fixed and immutable (the value is fixed).;

    . It is not allowed to create new instances with the new keyword;

    . The constructor is declared private, although it doesn't need an explicit private modifier;

    . Following the convention, as they are constant and immutable objects (static final),
    
    the declared names receive all letters in UPPERCASE;

    . Instances of enum types must have only one name;

    . Optionally, the class declaration can include instance variables, constructor,
    
    instance methods, class, etc.
      
      
Declaration of enums:
		
	public enum Letters {
		A, J, Q, K;
	}
	
Inicialization of enums:

	public enum CartasEnum {
		J(11),Q(12),K(13),A(14);

		public int valorCarta;

		CartasEnum(int valor) {
			valorCarta = valor;
		}
	}
      

Enum types can be used any time you need to represent a fixed set of constants.

Creation and invocation of an enum type:

	public enum MenuOptions {
		SAVE(1), PRINT(2), OPEN(3), VIEW(4), CLOSE(5);

		private final int valor;
			MenuOptions(int OptionValue){
			value = OptionValue;
		}
		
		public int getValue(){
			return value;
		}
	}
	
<!--End enum archive-->
<!--Init main archive that invokes the enums  -->

	public class EnumInv {
		public static void chooseOption(MenuOptions option){
			if(option == MenuOptions.SAVE){
				System.out.println("Saving file!");
			}
			else if(options == MenuOptions.OPEN){
				System.out.println("Opening file!");
			}
		}

			public static void main(String[] args) {
				chooseOption(MenuOptions.OPEN);
			}
	}

Examples of enums:

    package com.pernalonga.helpdesk.domain.enums;

    public enum Profile {
	
      ADMIN(0, "ROLE_ADMIN"), CLIENT(1, "ROLE_CLIENT"), TECNIC(2, "ROLE_TECNIC");

      private Integer code;
      private String description;

      private Profile(Integer code, String description) {
        this.code = code;
        this.description = description;
      }

      public Integer getCode() {
        return code;
      }

      public String getDescription() {
        return description;
      }

      public static Profile toEnum(Integer cod) {
        if(cod == null) {
          return null;
        }

        for(Profile x : Profile.values()) {
          if(cod.equals(x.getCode())) {
            return x;
          }
        }

        throw new IllegalArgumentException("Invalid profile");
      }

    }
