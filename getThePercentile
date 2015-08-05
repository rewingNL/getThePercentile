component output="false" {
	/**
	* @Hint:	Caculates the right percentile from a list with numbers
	* 
	* @param	numberList: list with numbers only with a ';' seperator; e.g.: "247427;148000;157200". (Required)
	* @param	percentileNumber: percentile number; between 0 and 100. (Required)
	* @param	kindOfPercentile: 'exc' or 'inc'; default: 'exc'.
	* @return	Returns a numeric value.
	* @author	René van Wingerden (r.v.wingerden@casema.nl)
	* @version	1, August 5, 2015
	* 
	*/
	public numeric function getThePercentile(string numberList, numeric percentileNumber, kindOfPercentile='exc') {
		var returnValue = 0;
		var percentileNumber = arguments.percentileNumber;
		var orderdedNumberList = listSort(arguments.numberList, 'numeric', 'asc', ';');
		var arrNumberlist = listToArray(orderdedNumberList, ';');
		var arrLen = arrayLen(arrNumberlist);

		try {
			if ((len(arrLen) and len(percentileNumber)) and (isNumeric(arrLen) and isNumeric(percentileNumber))) {
				if (arguments.kindOfPercentile eq 'inc') calculation  = ((((arrLen-2)*percentileNumber)+percentileNumber)/100)+1 ;
				else calculation  = ((arrLen*percentileNumber)+percentileNumber)/100 ;

				if (calculation lt 1) returnValue = 1
				else if (calculation gt arrLen) returnValue = arrLen;
				else returnValue = calculation;

				if (isNumeric(returnValue)) {
					var floorNumber = int(returnValue);
					var ceilingNumber = ceiling(returnValue);
					var floorAmount = arrNumberlist[floorNumber];
					var ceilingAmount = arrNumberlist[ceilingNumber];
					if (floorAmount neq ceilingAmount) {
						returnValue = floorAmount+((ceilingAmount-floorAmount)*(calculation-floorNumber));
					}
					else returnValue = floorAmount;
				}
			}
		} catch(any a) { returnValue = 0 ; }

		return returnValue;
	}
}
