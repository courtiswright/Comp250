
	public Number convert(Number A, short Base) {
		
		Number N0 = new Number();
		
		//initialize attributes of Number
		//others for testing purposes
		short R = Base;
		short Base1 = A.Base;
		short[] Int = A.Int;
//		short Base = 60;
//		short[] Int = {16,7,55,41};
		
		//convert Int of A and set result to be Int of N0
		short[] testy = ConvertInt(R, Base1, Int);
		N0.Int = testy;
		
		//return Number just created
		return N0;
	}
	
	public short[] ConvertInt(short R, short Base, short[] Int) {
		//declare variables for original base to base 10 conversion
		short Shortin10 = 0;
		String string;
		short toShort;
		
		//convert given Int in given base to same value in base 10
		for (int i=0; i<(Int.length); i++) {
			Shortin10 = (short) (Shortin10 + (short) (Int[i]*Math.pow(Base, (Int.length-1)-i)));
		}
		
		//declare variables for type manipulation of Int in base 10
		string = Short.toString(Shortin10);
		String [] stringArray = new String[string.length()];
		short[] Intin10 = new short[string.length()];
		
		//type manipulation to get answer in base 10 into short array form
		stringArray = string.split("");
		for (int i = 0; i<string.length(); i++) {
			toShort = Short.parseShort(stringArray[i]);
			Intin10[i] = toShort;
		}
		
		//declare variables for base 10 to result base conversion
		int temp = 0;
		short[] tempRemainder = {0};
		short[][] resultAndRemainders;
		java.util.ArrayList<Short> resultList = new java.util.ArrayList<Short>();
		
		//repeated long division to give result and remainders of each execution of longDivision
		//stores result temporarily to use in next iteration and adds remainder to ArrayList
		while (Intin10[Intin10.length-1] != 0) {
			resultAndRemainders = longDivision(Intin10, R);
			Intin10 = resultAndRemainders[0];
			tempRemainder = resultAndRemainders[1];
			
			temp = (int) (tempRemainder[0]);
			
			resultList.add((short) temp);
		}
		
		//type manipulation to get final answer in short array form
		java.util.Collections.reverse(resultList);
		short[] convertedInt = new short[resultList.size()];
		for (int i=0; i<resultList.size(); i++) {
			convertedInt[i] = resultList.get(i).shortValue();
		}
		
		//returns fully converted Int as array of shorts
		return convertedInt;
	}
	
	public short[][] longDivision(short[] number, int divisor) {

		//declare variables
		java.util.ArrayList<Short> remainders = new java.util.ArrayList<Short>();
		java.util.ArrayList<Short> result = new java.util.ArrayList<Short>();
		short[][] resultAndRemainders = new short[2][];
		int temp = 0;
		
		//divides repeatedly as in long division for every digit of original number
		//keeps track of temporary remainder in temp variable and adds result digits as it goes
		//at the end of the division, adds remainder to remainders ArrayList
		//accounts for numbers up to two digits (largest would be 69)
		for (int i=0; i<number.length; i++) {
			int dividend;
			if(number[i]<10) {
				dividend = number[i] + (temp*10);
			}
			else {
				dividend = number[i] + (temp*100);
			}
			 result.add((short) (dividend/divisor));
			 
			 if (i==0) {
				 temp = number[i]%divisor;
			 }
			 else {
				 temp = dividend%divisor;
			 }
		}
		remainders.add((short) temp);
		
		//type manipulation for result
		short[] resultArray = new short[result.size()];
		for (int i=0; i<resultArray.length;i++) {
			resultArray[i] = result.get(i);
		}
		
		//type manipulation for remainder
		short[] remainderArray = new short[remainders.size()];
		for (int i=0; i<remainderArray.length;i++) {
			remainderArray[i] = remainders.get(i);
		}
		
		//put result and remainder arrays into two dimensional array
		resultAndRemainders[0] = resultArray;
		resultAndRemainders[1] = remainderArray;

		//return two dimensional array composed of result of division and remainder of division
		return resultAndRemainders;
	}

