FlyWeight 패턴

- FlyWeight

  - 복싱_'플라이급'은 매우 가볍다.
  - 자바 
    - 메모리 사용량이 적다.
    - 이미 만들어져있는 것은 공유시키고 데이터가 없을때만 객체를 새로 생성함.

- 실생활에 Flyweight가 존재 할때 예제 

  -  성탄절이 다가왔다. 산타할아버지는 재정난에 시달렸지만 아이들에게 인형을 주려고 한다. 인형 하나만 구입하고도 여러개인형을 만들어준다고하여 Flyweight마법사를 고용하게되었다. 

  - 구현 코드

    ```
    public interface Toy {
        void finished();
    }
    
    public class Doll implements Toy {
    
        private String name;
        private String color;
    
        public Doll(String name) {
            this.name = name;
        }
    
        public void setColor(String color) {
            this.color = color;
        }
    
        @Override
        public void finished() {
            System.out.println("Toy: finished() [name : " + name + ", color : " + color);
        }
    
    }
    public class ToyFactory {
    
        static Map<String, Doll> dollMap = new HashMap();
    
        public static Doll getDoll(String toyName) {
            Doll doll = dollMap.get(toyName);
            if (doll == null) {
                doll = new Doll(toyName);
                dollMap.put(toyName, doll);
                System.out.println("Shanta bought a toy->" + toyName);
            }
            return doll;
        }
    }
    public class FlyweightWizard {
        private static final String[] dollNames = {"Penguin", "Pokemon", "Apitch", "Ryan"};
        private static final String[] colors = {"Red", "Gree", "Blue", "White", "Black"};
    
        public static void main(String[] args) {
            for (int i = 0; i < 20; i++) {
                Doll doll = ToyFactory.getDoll(getRandomName());
                doll.setColor(getRandomColor());
                doll.finished();
            }
        }
    
        private static String getRandomName() {
            return dollNames[(int) (Math.random() * dollNames.length)];
        }
    
        private static String getRandomColor() {
            return colors[(int) (Math.random() * colors.length)];
        }
    
    }
    
    ```

  - UML
  ![UML](https://drive.google.com/file/d/1qujBK2jKJkqRSKXby0KepasPD0-b5HLb/view?usp=sharing)

- 기타 구현 예제

  - IntegerClass

    ```
    private static class IntegerCache {
    
        static final int low = -128;
    
        static final int high;
    
        static final Integer cache[];
    
    
        static { // static으로 실행되기 때문에 실행 이전에 생성이 완료됨.
    
            // high value may be configured by property
    
            int h = 127;
    
            String integerCacheHighPropValue =
    
                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
    
            if (integerCacheHighPropValue != null) {
    
                try {
    
                   int i = parseInt(integerCacheHighPropValue);
    
                   i = Math.max(i, 127);
    
                   // Maximum array size is Integer.MAX_VALUE
    
                   h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
    
               } catch( NumberFormatException nfe) {
    
                   // If the property cannot be parsed into an int, ignore it.
    
               }
    
            }
    
            high = h;
    
    
            cache = new Integer[(high - low) + 1]; // Flyweight 생성 부분
    
            int j = low;
    
            for(int k = 0; k < cache.length; k++)
    
                cache[k] = new Integer(j++);
    
    
            // range [-128, 127] must be interned (JLS7 5.1.7)
    
            assert IntegerCache.high >= 127;
    
        }
    
    
        private IntegerCache() {}
    
    }
    
    
    public static Integer valueOf(int i) {  // Flyweight 객체 제공 부분
    
        if (i >= IntegerCache.low && i <= IntegerCache.high)
    
            return IntegerCache.cache[i + (-IntegerCache.low)];
    
        return new Integer(i);
    
    } 
    
    ```

- 언제 사용해야하는가?

  - 중복 생성될 가능성이 높은 경우.

    중복 생성될 가능성이 높다는 것은 동일한 자원이 자주 사용될 가능성이 매우 높다는 것을 의미한다. 이런 자원은 공통 자원 형태로 관리하고 있다가 요청이 있을 때 제공해 주는 편이 좋다.

  - 자원 생성 비용은 큰데 사용 빈도가 낮은 경우.

    이런 자원을 항상 미리 생성해 두는 것은 낭비이다. 따라서 요청이 있을 때에 생성해서 제공해 주는 편이 좋다.

    이 두가지 목적을 위해서 Flyweight 패턴은 자원 생성과 제공을 책임진다. 자원의 생성을 담당하는 Factory 역할과 관리 역할을 분리하는 것이 좋을 수 있으나, 일반적으로는 두 역할의 크기가 그리 크지 않아서 하나의 클래스가 담당하도록 구현한다.

- 내가 생각했을때의 현업 예제

  - 병원 예약 내역 및 취소하는 기능 구현
    - 각 지점별 의사 정보 DB(의사인덱스, 병원이름, 의사이름, 의사약력.....)
    - 예약정보(의사인덱스, 예약날짜, 취소여부, 취소한날짜)
    - 문제점 : 하나의 화면에 서버 주소가 달라서 따로 가져와야하는 상황 발생
    - 해결방법 : 의사정보를 다 받아온 후 Flyweight패턴이용하여 의사 인덱스를 키 값으로 둬서 HashMap형태 만들고 예약정보 가져올때마다 대입함 .

- 참고

  - [디자인패턴UML](https://kevinx64.net/173)
  - [Flyweight패턴-실생활예제](https://ncanis.tistory.com/103)
  - [Integer-flyweight패턴](https://effectiveprogramming.tistory.com/entry/Flyweight-%ED%8C%A8%ED%84%B4)
